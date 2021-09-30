<!-- 5.4 -->

This command uses the scheduling system to collect data from device interfaces and orders rules applied against collected monitored data. 

For detailed information about writing and using monitors, refer to the Guide to Rules and Monitors. 

# Command availability 

CLI resource: All

Device makes: All

Modem : All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config monitors <"object"> <"instanceName"> ["ruleList"] [:"delay"]

```

objects may be:

- **chassis** (port resource)
- **circuit** (powercontrol resource)
- **consoleLog** (port resource)
- **interface** (port resource)
- **modem** (modem resource)
- **ping** (port resource)
- **remotestate** (port resource)
- **slv** (system resource) A valid SLV license is required for this command.
- **sms** (modem resource)
- **terminal** (port resource)

The instanceName is used with the interface object; it specifies an interface on a network device. Examples:

- **Ethernet0/0**
- **FastEthernet0**
- **Serial1**

**ruleList** - Optional; accepts rules and rulesets. Separate rules and rulesets by commas and pipes (|).

"**delay**" - Specify a time in seconds between executions. Default time is 30 seconds. 

# Usage 

Data collection takes approximately 3 seconds per interface, so the maximum number of interfaces that can be reliably monitored at 30-second (default) intervals is 10. To increase the number of interfaces logged, increase the interval to allow at least 3 seconds for each interface.

Incorrect interfaces will respond with "% Invalid input detected at '^' marker." and/or "Bad argument encountered" and the monitor will remain unscheduled.

```
[admin@UplogixLM (port1/1)]# config monitor interface Ethernet0/0 LinkAggrigation,defaultEthernetRule :45
Job was scheduled 14: [Interval: 00:00:45 Mask: * * * * *] showInterface Ethernet0/0
```

To monitor whether the embedded modem has a good connection, use the built-in modemLineDisconnected rule:

```
[admin@UplogixLM ]# modem
[admin@UplogixLM (modem)]# config monitors modem modemLineDisconnected :30
Job was scheduled 0: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor modem embedded modemLineDisconnected 30 
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > Local Manager page > Scheduled Tasks > schedule button** - specific to this Local Manager

**Inventory > Local Manager page > port detail > schedule button** - specific to this device

# History 

1.02 - Requirement for interface type parameter removed.

1.1 - Added rule subsystem commands and new command syntax.

2.5 - Command now available on modem resource.

3.3 - Command now available on powercontrol resource; added circuit object.  
Added sms object for modem.

# Related commands 

- **config rule**
- **config ruleset**
- **show monitors**
- **config removejob**
