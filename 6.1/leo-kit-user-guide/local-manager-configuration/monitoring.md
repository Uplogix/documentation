The Local Manager's monitoring system can be used to ensure the modem's availability during a network outage. This section provides rules for monitoring signal quality, error messages, network availability, and general responsiveness.

# Monitoring Error Messages

When the default modem monitor is scheduled, a series of commands are run on the Iridium modem. This rule generates an alarm if the response to any of those commands is ERROR.

```
config rule iridiumErrorMessage
action alarm -a "Iridium modem returning errors"
conditions
modem.response matches "ERROR":2i
exit
exit
```

Use the **config monitor modem** command to start using these rules:

```
[admin@UplogixLM (modem)]# config monitor modem iridiumErrorMessage :120
```

# Monitoring Signal Quality (passive)

Consistent signal quality is imperative to the reliable operation of the Iridium modem. Use the following rule to generate an alert whenever signal quality drops below a minimum value.

```
config rule iridiumSignalQuality
action alarm -a "Iridium Signal Quality below recommended"
conditions
NOT modem.response matches "CSQ:[4-5]":2i
exit
exit
```

This rule examines the value of *modem.response*, which is populated by the AT+CSQ? command automatically. If the signal quality drops below 4, an alarm will be generated. This rule can be relaxed by changing the numbers in the square brackets.

To only alert when the signal quality drops to zero, use:

```
NOT modem.response matches â€œCSQ:[1-5]â€:2i
```

The :2i argument indicates that the appliance should wait for two intervals of CSQ less than 1 before generating an alarm.

Use the **config monitor modem** command to start using these rules. Additional rules can also be specified:

```
[admin@UplogixLM (modem)]# config monitor modem iridiumErrorMessage, iridiumSignalQuality :120
```

# Monitoring Signal Quality (active)

While low signal quality alone is not cause for a reboot, the presence of ERROR messages may indicate a problem with the Iridium modem or network. The following rule will power cycle the modem if for ten minutes: A) signal quality remains at 0 or B) AT commands result in ERROR messages.

```
config rule iridiumServiceCheck
action alarm -a "Iridium Service Unavailable for 10 minutes, powercycling"
action powerCycle
conditions
modem.response matches "ERROR":10m OR
NOT modem.response matches "CSQ:[1-5]":10m
exit
exit
```

Use the **config monitor modem** command to start using these rules. Additional rules can also be specified:

```
[admin@u3200 (modem)]# config monitor modem iridiumErrorMessage, iridiumSignalQuality, iridiumServiceCheck :120
```

# Displaying Signal Quality on Front Panel (u5000)

Using the action writeStatus command, you can have the current CSQ value displayed on the LMâ€™s front LCD screen. This can be useful for onsite personnel who donâ€™t have access to the CLI.

Create the following rules on your Control Center or Local Manager:

```
config rule iridiumCSQ0
action writeStatus CSQ is 0
conditions
modem.response matches "CSQ:0"
exit
exit

config rule iridiumCSQ1
action writeStatus CSQ is 1
conditions
modem.response matches "CSQ:1"
exit
exit

config rule iridiumCSQ2
action writeStatus CSQ is 2
conditions
modem.response matches "CSQ:2"
exit
exit

config rule iridiumCSQ3
action writeStatus CSQ is 3
conditions
modem.response matches "CSQ:3"
exit
exit

config rule iridiumCSQ4
action writeStatus CSQ is 4
conditions
modem.response matches "CSQ:4"
exit
exit

config rule iridiumCSQ5
action writeStatus CSQ is 5
conditions
modem.response matches "CSQ:5"
exit
exit
```

Create a rule set to make scheduling easier:

```
config ruleset iridiumCSQ
rules
iridiumCSQ0 | iridiumCSQ1 | iridiumCSQ2 | iridiumCSQ3 | iridiumCSQ4 | iridiumCSQ5
exit
exit

```

Use the **config monitor** command to use these rules:

```
[admin@UplogixLM (modem)]# config monitor modem iridiumCSQ :120
```