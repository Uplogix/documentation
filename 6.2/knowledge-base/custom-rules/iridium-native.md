<!-- 5.4 -->

The following ruleset is designed to monitor the signal strength of the Iridium satellite modem and will power cycle the modem if it becomes unresponsive.

In order for the powercycle portion of the ruleset to work, the Local Manager must have a power controller installed and an outlet mapped for the modem. You will then need to paste the following into the CLI on the system resource.

```
config rule iridiumErrorMessage
action alarm -a "Iridium modem returning errors"
conditions
modem.response matches "ERROR" :2i
exit
exit

config rule iridiumNonResponsive
action alarm -a "the console has become unusable for 10 minutes, powercycling"
action event GENERIC -a "the console has become unusable for 10 minutes,  powercycling"
action powerCycle
conditions
modem.response equals FAILED_TO_GET_RESPONSE :13i AND
NOT has-run powerCycle :15m
exit
exit

config rule iridiumServiceUnavailableForTenMinutesPowerCycle
action alarm -a "Iridium Service Unavailable for 10 minutes, powercycling"
action event GENERIC -a "Iridium Service Unavailable for 10 minutes (signal 0), powercycling"
action powerCycle
conditions
modem.response matches "ERROR" :13i AND
NOT has-run powerCycle :15m
exit
exit

config rule iridiumSignalQuality
action alarm -a "Iridium Signal Quality below minimum"
conditions
modem.response matches "CSQ:0" :2i
exit
exit

config rule iridiumSignalQualityAt0
action writeStatus SigStrngth is 0
conditions
modem.response matches "CSQ:0"
exit
exit

config rule iridiumSignalQualityAt1
action writeStatus SigStrngth is 1
conditions
modem.response matches "CSQ:1"
exit
exit

config rule iridiumSignalQualityAt2
action writeStatus SigStrngth is 2
conditions
modem.response matches "CSQ:2"
exit
exit

config rule iridiumSignalQualityAt3
action writeStatus SigStrngth is 3
conditions
modem.response matches "CSQ:3"
exit
exit

config rule iridiumSignalQualityAt4
action writeStatus SigStrngth is 4
conditions
modem.response matches "CSQ:4"
exit
exit

config rule iridiumSignalQualityAt5
action writeStatus SigStrngth is 5
conditions
modem.response matches "CSQ:5"
exit
exit

config ruleset iridiumNative
description null
rules
iridiumNonResponsive | iridiumSignalQualityAt0 | iridiumSignalQualityAt1 | iridiumSignalQualityAt2 | iridiumSignalQualityAt3 | iridiumSignalQualityAt4 | iridiumSignalQualityAt5 | iridiumSignalQuality |  iridiumServiceUnavailableForTenMinutesPowerCycle | iridiumErrorMessage
exit
exit 
```

Use the **config monitor modem** command to activate this ruleset on the modem resource.

```
[admin@UplogixLM (modem)]# config monitor modem iridiumNative
```

Further reading: [LEO-I Kit User Guide](/docs/leo-kit-user-guide/)