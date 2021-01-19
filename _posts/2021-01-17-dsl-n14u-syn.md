---
layout: post
title: "Nmap, the silent slayer"
date: 2021-01-20
comments: true
categories: vulnerability
---


## Affected products

We have not yet tested Asus models other than those listed. However we suspect it may also work on other models with the same firmware version.

```
    DSL-N14U_B1 V.1.1.2.3_805
    
```




## Overview

An issue was discovered on ASUS DSL-N14U-B1 1.1.2.3_805 device. Remote attacker to cause a denial of service (crash) by performing a SYN scan using a tool such as nmap. Sending these packets causes a persistent outage of the jetdirect (9100/tcp), LPD (515/tcp) and sos (3838/udp) services. 

## POC

**This PoC can crash services.**

**Given the vendor's security, we don't show the service execution flow, however we will explain the vulnerability in a comprehensive way.**


We enter the router via ssh to understand through the proc file system what happens.

![](/assets/asus_2/raw_socket_before.png)

Come mostrato in figura, possiamo notare dei servizi attivi e la loro porta in formato esadecimale.
Quelli che ci interessano sono sostanzialmente 515 (jetdirect) nonché 0203, 
e 515 (LPD) che corrisponde a 238C in esadecimale.

Lanciamo nmap inserendo uno script relativamente intrusivo. Come riportato dal sito di nmap (https://nmap.org/book/nse-usage.html), the more intrusive a script is, the more it engages the services until they crash (as in this case).

`nmap -sV --script pjl-ready-message -p 9100 192.168.1.1`


Una volta eseguito, noteremo immediatamente delle differenze nel proc file system.

![](/assets/asus_2/raw_socket_after.png)


Come controprova, mostriamo lo stato dei servizi prima e dopo l'esecuzione di nmap via `netstat -tulen` 
(busybox non supporta -p, motivo per cui lavoriamo sul proc file system all'interno del router).

![](/assets/asus_2/netstat_before.png)

![](/assets/asus_2/netstat_after.png)

Verifichiamo inoltre se ci sono stati altri servizi locali non visibili per le policy del firewall ad essere stati compromessi. Per facilitarne la comprensione, confrontiamo le due immagini.

![](/assets/asus_2/tcp_udp_all_before.png)

![](/assets/asus_2/tcp_udp_all_after.png)

Se avete avuto occhio in precedenza  avete visto bene, sono ben tre ocorrenze ad essere eliminate...
Un altro servizio è crashato...sos service (3838/tcp) - Scito Object Server

I servizi torneranno attivi solo con un intervento fisico (reboot)



Dato il contesto limitante di un ambiente come quello di un router, vi consiglio per "abbellire" il formato del proc file system da questo articolo https://staaldraad.github.io/2017/12/20/netstat-without-netstat/).
