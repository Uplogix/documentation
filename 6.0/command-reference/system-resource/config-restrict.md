<!-- 5.4 -->

Restricts actions automatically called by rules to predefined thresholds. Each action can be restricted by port, minimum interval or an eligible time window. For example, a reboot may be called by a rule but be cancelled because a reboot has occurred within the past 3 hours. The reboot will not execute outside the cron-time mask, if one has been set.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config restrict [no] <"actionName"> ["port"] [-i <#>] [-m <time>]
```

Options:

**[no]** - remove existing restrictions on this action.

**port#** - restrict the action only on this port.

**-i** - minimum interval in seconds before this action executes again.

**-m <time>** - specifies when the action may execute, in cron format. For example, * * * * 6-0 restricts the specified action to occur only on Saturdays (day 6) and Sundays (day 0).

For information about using cron format, see About cron format 

The jobs that can be restricted depend on what can be scheduled on the device. The following jobs are defined:

- **assimilate** - Assimilate a device. 
- **certify** - Copies working directory contents to certified (Alcatel).
- **clearCounters** - Clears all interface counters.
- **clearServiceModule** - Clears the service module.
- **deviceInfo** - Collects device serial number, make, model, and OS information.
- **interfaceCycle** - Cycles the interface specified.
- **interfaceOff** - Turns off the interface specified.
- **interfaceOn** - Turns on the interface specified.
- **pppOff** - Turn PPP off.
- **pppOn** - Turn PPP on.
- **pullOS** - Copies an OS image from the device to the system.
- **pullRunningConfig** - Copies a running config file from the specified device to the system.
- **pullStartupConfig** - Copies a startup config file from the specified device to the system.
- **pushOS**  - Push an OS image to the specified device.
- **pushRunningConfig** - Push a running config to the specified device.
- **pushStartupConfig** - Push a startup config to the specified device.
- **reboot** - Reboot the device connected to this port. 
- **rebootAll** - Reboot the stack to which this device belongs (Alcatel).
- **rebootWorking** - Reboot the device from the working configuration (Alcatel).
- **recoverPassword** - Forces restore of last known startup.
- **restore** - Copies certified directory contents to working (Alcatel).
- **showTech** - Collect tech support information from the specified device.
- **writememory** - Saves running config. 

# Usage 

The event action inside a rule can override restrictions with an optional force flag.

This example restricts cycling power to no more than every 3 hours. The -i interval parameter is given in seconds.


```
[admin@UplogixLM]# config restrict powerCycle -i 10800
```

This example restricts rebooting port 1/4 except on weekends:

```
[admin@UplogixLM]# config restrict reboot port1/4 -m "* * * * 0,6"
```

# History 

1.1 - This command was introduced.

# Related commands 

- **config rule**
- **show restrict**
