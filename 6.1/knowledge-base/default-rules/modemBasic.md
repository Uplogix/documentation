# Overview

Uplogix Local Managers ship with a default ruleset for monitoring v.92 modems. The primary goal of this ruleset is to ensure out-of-band is available when it is needed.

# Ruleset

The default ruleset is called *modemBasic*.

```
[admin@UplogixLM]# show ruleset modemBasic
ruleset modemBasic
description Rules for testing the internal modem
rules
modemLineInUse | modemLineDisconnected

exit
exit
```

Two rules are included in *modemBasic*:

* modemLineInUse
* modemLineDisconnected

This ruleset is used in conjunction with the modem monitor and examines the responses received from the modem.

# Rules

Let's take a closer look at each rule.

## modemLineInUse

```
rule modemLineInUse
action alarm MODEM_LINE_IN_USE
conditions
modem.response equals "LINE IN USE" :2i
exit
exit
```

This rule looks for the response *LINE IN USE* and throws an alarm if detected. The *2i* modifier instructs the Local Manager to wait two intervals before throwing an alarm.

Since the modem line should only be in use when the Local Manager is operating out-of-band, this rule will help identify a problem that may prevent dial-in or dial-out when needed.

## modemLineDisconnected

```
[admin@UplogixLM]# show rule modemLineDisconnected
rule modemLineDisconnected
action alarm MODEM_LINE_DISCONNECTED
conditions
modem.response equals "NO DIALTONE" :2i OR
modem.response equals "NO LINE" :2i OR
modem.response matches "1\.40\s+OK" :2i
exit
exit
```

This rule looks for multiple responses that may indicate a problem with the attached phone line. The *2i* modifier instructs the Local Manager to wait two intervals before throwing an alarm

* NO DIALTONE - the modem was unable to detect a dialtone when dialing
* NO LINE - the modem was unable to detect a line when dialing
* `1\.40\s+OK` - ??

Any of the above responses are good indications that out-of-band may fail when initiated. Use this rule to get notified of problems and fix them before a network outage.

# Scheduling

Modem monitors are not scheduled by default, but are recommended for all Local Managers that rely on v.92 for out-of-band access.

To schedule the modem monitor with the modemBasic ruleset, log into the Local Manager and change to the modem resource.

Use the **config monitor modem** command to schedule the monitor. Use the following syntax:

```
[super@UplogixLM (modem)]# config monitor modem modemBasic
Validate scheduled monitor(modem)?  (This will execute the job now.) (y/n): y
Job was scheduled 8: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor modem none modemBasic 30
```

