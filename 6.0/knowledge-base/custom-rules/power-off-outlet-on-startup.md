<!-- 5.4 -->

# Problem

Basic models of the ServerTech power controller do not support the wake state found in more advanced models. The wake state allows you to configure what status your outlets should have when the power controller is turned on or when it recovers from a power failure.

# Solution

Use a rule to power off the appropriate outlet when the appliance starts up. This assumes that a reset equals a power failure, so this may not be useful in all scenarios. In this example, we will create a rule that will power off the Cisco Router on port 1/1.

# Create a Rule

Create a rule called initialOff from the Control Center or Local Manager command line.

```
[admin@UplogixLM]# config rule initialOff
[config rule initialOff]# conditions
[config rule initialOff conditions]# NOT has-value monitor io_status
[config rule initialOff conditions]# exit
[config rule initialOff]# action powerOff
[config rule initialOff]# action setValue monitor io_status 1
[config rule initialOff]# exit
```

# How Does it Work?

This rule makes use of a state variable called io_status. While this rule is executing, this variable will have two values: "unitialized" and "1". When the variable is unitialized (has no value), the rule will execute the powerOff action. It will also execute the setValue action, which will change the io_status variable's value from unitialized to 1. Once this variable has a value, the rule will no longer evaluate as true, which prevents powerOff from running every 30 seconds.

# Apply the Rule

This rule can be added to the default chassis monitor on any port that has power outlets mapped. Simply replace the default monitor with the new one:

```
[admin@UplogixLM (port1/1)]# config monitor chassis initialOff
PWR: Powering off powercontrol outlet(s) [A1]
PWR: DSR was active.
PWR: CTS was active.
Cancelling previous monitor for 'chassis none'
Job was scheduled 19: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor chassis none initialOff 30
```

Power is immediately turned off because at the time the monitor was first run, the io_status variable was uninitialized. This will also be the case when the appliance first boots following a restart or a power failure.