Schedule this ruleset as a remotestate monitor on your Comtech.

```
config rule no ebno0to2
config rule ebno0to2
action writeStatus EbNo < 2db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo min 1.9
exit
exit

config rule no ebno2to4
config rule ebno2to4
action writeStatus EbNo 2 - 4 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo min 2
remotestate.remoteEbNo min 3.9
exit
exit

config rule no ebno4to6
config rule ebno4to6
action writeStatus EbNo 4 - 6 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 4.0 AND
remotestate.remoteEbNo min 5.9
exit
exit

config rule no ebno6to8
config rule ebno6to8
action writeStatus EbNo 6 - 8 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 6.0 AND
remotestate.remoteEbNo min 7.9
exit
exit

config rule no ebno8to10
config rule ebno8to10
action writeStatus EbNo 8 - 10 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 8.0 AND
remotestate.remoteEbNo min 9.9
exit
exit

config rule no ebno10to12
config rule ebno10to12
action writeStatus EbNo 10 - 12 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 10.0 AND
remotestate.remoteEbNo min 11.9
exit
exit

config rule no ebno12to14
config rule ebno12to14
action writeStatus EbNo 12 - 14 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 12.0 AND
remotestate.remoteEbNo min 13.9
exit
exit

config rule no ebno14to16
config rule ebno14to16
action writeStatus EbNo 14 - 16 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 14.0 AND
remotestate.remoteEbNo min 15.9
exit
exit

config rule no ebno16orMore
config rule ebno8orMore
action writeStatus EbNo > 16 db
conditions
remotestate.receiverLock equals true AND
remotestate.remoteEbNo max 16
exit
exit

config rule no comtechUnlocked
config rule comtechUnlocked
action writeStatus Unlocked
conditions
remotestate.receiverLock equals false
exit
exit

config ruleset no comtechLocked
config ruleset comtechLocked
description null
rules
ebno0to2, ebno2to4, ebno4to6. ebno6to8. ebno8to10, ebno10to12, ebno12to14,ebno14to16, ebno16orMore
exit
exit

config ruleset no comtechNative
config ruleset comtechNative
description null
rules
comtechUnlocked, comtechLocked
exit
exit
```