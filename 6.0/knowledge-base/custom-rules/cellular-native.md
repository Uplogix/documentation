<!-- 5.4 -->

The following rules read and report cellular signal strength and reboot the modem if it returns an error.

The ruleset can be configured on the Local Manager modem resource with the command **config monitor modem CellularNative**.

```
config rule no CellularSignalQuality0
config rule CellularSignalQuality0
description Cellular Signal QualityAt0
action alarm -a "Cellular Signal Quality below minimum"
action writeStatus Cell % is 0
conditions
modem.response matches "CSQ:\s0,"
exit
exit

config rule no CellularSignalQuality1
config rule CellularSignalQuality1
description Cellular Signal QualityAt1
action alarm -a "Cellular Signal Quality below minimum"
action writeStatus Cell % is 1
conditions
modem.response matches "CSQ\s1,"
exit
exit

config rule no CellularSignalQuality2
config rule CellularSignalQuality2
description Cellular Signal QualityAt2
action alarm -a "Cellular Signal Quality below minimum"
action writeStatus Cell % is 2
conditions
modem.response matches "CSQ:\s2,"
exit
exit

config rule no CellularSignalQuality3
config rule CellularSignalQuality3
description Cellular Signal QualityAt3
action alarm -a "Cellular Signal Quality below minimum"
action writeStatus Cell % is 3
conditions
modem.response matches "CSQ:\s3,"
exit
exit

config rule no CellularSignalQuality4
config rule CellularSignalQuality4
description Cellular Signal QualityAt4
action alarm -a "Cellular Signal Quality below minimum"
action writeStatus Cell % is 4
conditions
modem.response matches "CSQ:\s4,"
exit
exit

config rule no CellularSignalQuality5
config rule CellularSignalQuality5
description Cellular Signal QualityAt5
action alarm -a "Cellular Signal Quality below minimum"
action writeStatus Cell % is 5
conditions
modem.response matches "CSQ:\s5,"
exit
exit

config rule no CellularSignalQuality6
config rule CellularSignalQuality6
description Cellular Signal QualityAt6
action writeStatus Cell % is 6
conditions
modem.response matches "CSQ:\s6,"
exit
exit


config rule no CellularSignalQuality7
config rule CellularSignalQuality7
description Cellular Signal QualityAt7
action writeStatus Cell % is 7
conditions
modem.response matches "CSQ:\s7,"
exit
exit

config rule no CellularSignalQuality8
config rule CellularSignalQuality8
description Cellular Signal QualityAt8
action writeStatus Cell % is 8
conditions
modem.response matches "CSQ:\s8,"
exit
exit

config rule no CellularSignalQuality9
config rule CellularSignalQuality9
description Cellular Signal QualityAt9
action writeStatus Cell % is 9
conditions
modem.response matches "CSQ:\s9,"
exit
exit

config rule no CellularSignalQuality10
config rule CellularSignalQuality10
description Cellular Signal QualityAt10
action writeStatus Cell % is 10
conditions
modem.response matches "CSQ:\s10,"
exit
exit

config rule no CellularSignalQuality11
config rule CellularSignalQuality11
description Cellular Signal QualityAt11
action writeStatus Cell % is 11
conditions
modem.response matches "CSQ:\s11,"
exit
exit

config rule no CellularSignalQuality12
config rule CellularSignalQuality12
description Cellular Signal QualityAt12
action writeStatus Cell % is 12
conditions
modem.response matches "CSQ:\s12,"
exit
exit

config rule no CellularSignalQuality13
config rule CellularSignalQuality13
description Cellular Signal QualityAt13
action writeStatus Cell % is 13
conditions
modem.response matches "CSQ:\s13,"
exit
exit

config rule no CellularSignalQuality14
config rule CellularSignalQuality14
description Cellular Signal QualityAt14
action writeStatus Cell % is 14
conditions
modem.response matches "CSQ:\s14,"
exit
exit

config rule no CellularSignalQuality15
config rule CellularSignalQuality15
description Cellular Signal QualityAt15
action writeStatus Cell % is 15
conditions
modem.response matches "CSQ:\s15,"
exit
exit

config rule no CellularSignalQuality16
config rule CellularSignalQuality16
description Cellular Signal QualityAt16
action writeStatus Cell % is 16
conditions
modem.response matches "CSQ:\s16,"
exit
exit

config rule no CellularSignalQuality17
config rule CellularSignalQuality17
description Cellular Signal QualityAt17
action writeStatus Cell % is 17
conditions
modem.response matches "CSQ:\s17,"
exit
exit

config rule no CellularSignalQuality18
config rule CellularSignalQuality18
description Cellular Signal QualityAt18
action writeStatus Cell % is 18
conditions
modem.response matches "CSQ:\s18,"
exit
exit

config rule no CellularSignalQuality19
config rule CellularSignalQuality19
description Cellular Signal QualityAt19
action writeStatus Cell % is 19
conditions
modem.response matches "CSQ:\s19,"
exit
exit

config rule no CellularSignalQuality20
config rule CellularSignalQuality20
description Cellular Signal QualityAt20
action writeStatus Cell % is 20
conditions
modem.response matches "CSQ:\s20,"
exit
exit

config rule no CellularSignalQuality21
config rule CellularSignalQuality21
description Cellular Signal QualityAt21
action writeStatus Cell % is 21
conditions
modem.response matches "CSQ:\s21,"
exit
exit

config rule no CellularSignalQuality22
config rule CellularSignalQuality22
description Cellular Signal QualityAt22
action writeStatus Cell % is 22
conditions
modem.response matches "CSQ:\s22,"
exit
exit

config rule no CellularSignalQuality23
config rule CellularSignalQuality23
description Cellular Signal QualityAt23
action writeStatus Cell % is 23
conditions
modem.response matches "CSQ:\s23,"
exit
exit

config rule no CellularSignalQuality24
config rule CellularSignalQuality24
description Cellular Signal QualityAt24
action writeStatus Cell % is 24
conditions
modem.response matches "CSQ:\s24,"
exit
exit

config rule no CellularSignalQuality25
config rule CellularSignalQuality25
description Cellular Signal QualityAt25
action writeStatus Cell % is 25
conditions
modem.response matches "CSQ:\s25,"
exit
exit

config rule no CellularSignalQualityAbove25
config rule CellularSignalQualityAbove25
description Cellular Signal QualityAt25
action alarm -a "Cellular modem RSSI Above 25"
action writeStatus Cell % is > 25
conditions
modem.response matches "CSQ:\s(?:(?:[2][5-9])|(?:[3-9][0-9])),"
exit
exit

config rule no CellularErrorMessage
config rule CellularErrorMessage
description Cellular Error Message
action powerCycle
action alarm -a "Cellular modem returning errors"
conditions
modem.response matches "ERROR":2i AND
NOT has-run powerCycle :5m
exit
exit

config rule CellularNonResponsive
action alarm -a "the modem has become unusable for 5 minutes, powercycling"
action event GENERIC -a "the modem has become unusable for 5 minutes,  powercycling"
action powerCycle
action writeStatus no response powercycling
conditions
modem.response equals FAILED_TO_GET_RESPONSE :10i AND
NOT has-run powerCycle :5m
exit
exit

config ruleset no CellularNative
config ruleset CellularNative
description Cellular Rules for Multitech GPRS Cell Modems
rules
CellularNonResponsive, CellularErrorMessage, CellularSignalQuality25, CellularSignalQuality24, CellularSignalQuality23, CellularSignalQuality22, CellularSignalQuality21, CellularSignalQuality20, CellularSignalQuality19, CellularSignalQuality18, CellularSignalQuality17, CellularSignalQuality16, CellularSignalQuality15, CellularSignalQuality14, CellularSignalQuality13, CellularSignalQuality12, CellularSignalQuality11, CellularSignalQuality10, CellularSignalQuality9, CellularSignalQuality8, CellularSignalQuality7, CellularSignalQuality6, CellularSignalQuality5, CellularSignalQuality4, CellularSignalQuality3, CellularSignalQuality2, CellularSignalQuality1, CellularSignalQuality0, CellularSignalQualityAbove25
exit
exit
```