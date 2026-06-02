
Initial Dump

Pure Free RAM (Empty space): 141,060K (Only about 141 MB is truly, completely empty).
Cached RAM (Apps on standby): 3,551,532K (About 3.5 GB of suspended apps).
Active Kernel Used: 2,058,684K (About 2.0 GB running the core OS).
Active PSS Used: 5,203,233K (About 5.2 GB running your active apps).
Lost Hardware RAM: 371,579K (About 0.36 GB for hardware components).

Many Xiaomi devices come with Google apps I don't use. These are usually safe to uninstall directly from the app drawer, but their package names are included here for completeness:

## com.mi.globalrowser
Privacy nightmare. You really should use something else.
https://www.xda-developers.com/xiaomi-mi-web-browser-pro-mint-collecting-browsing-data-incognito-mode/
Since MIUI 12, you can no longer uninstall this app. Disabling it still works fine.

## com.miui.msa.global
Analyzation of user behaviors to show you ads. Yeah Xiaomi phones has ads...
https://www.theverge.com/2018/9/19/17877970/xiaomi-ads-settings-menu-android-phones

## com.mi.analytics
According to a guy who tried to reverse engineer this app, Xiaomi Analytics can replace any (signed?) package they want silently on your device within 24 hours. Maybe that no longer the case now but... you don't want analytics anyway.
Source : http://blog.thijsbroenink.com/2016/09/xiaomis-analytics-app-reverse-engineered/

## com.mi.mipicks
Mi Picks (becomed Mi Apps Store and now Get Apps -- Xiaomi app store)

## com.xiaomi.mi_connect_service
Handles connection to IoT stuff Seems to be linked to Mi Home (com.xiaomi.smarthome)

## com.xiaomi.glgm
Xiaomi Games

## com.xiaomi.mtb
Rueban(MTB)V2.4
Hidden debugging baseband tools, not available for users.
https://i.postimg.cc/GpSxmNyj/Bez-n-zvu.png


## com.miui.daemon
Collects a lot of data and sends them to China.
See: https://web.archive.org/web/20210923050136/https://twitter.com/fs0c131y/status/938872347087564800

## com.miui.misightservice
Telemetry and diagnostics collector app that sends analytics to Xiaomi servers and has almost no use for user.
Something on the level of com.miui.msa or com.miui.daemon. Worth deleting.
Constantly connects somewhere and sends/receives up to 100KB of data per day to/from an unknown source. This also means it often runs in background.
It's labeled as Blur and has orange-white MI icon, but it just hides under it. No blur/ui/any other issues seen after around a month of use of HyperOS 2.0 with this removed.

## com.xiaomi.touchservice
No activities, uses miui analytics looks like a tracking touch.

com.xiaomi.xmfskeeper 
Xiaomi Service Framework Keeper
Logger service for 'com.xiaomi.xmsf'


## com.xiaomi.trustservice
MiTrustService - IFAASecCam, security things or 'Remote Control trust'.

