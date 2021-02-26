<!-- 5.5 -->
<!-- Description: Detect Active vs Standby status on an F5 using custom rules and Enhanced Native Mode-->

This document describes how to detect Active and Standby states on an F5 load balancer.

## Configure Port

Configure a port on the Local Manager using [Enhanced Native Mode](https://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/using-enhanced-native-mode). The following settings may need to be adjusted for your specific device:

```
command prompt [[#>]]: #
login prompt [sername:\s]: login:\s
password prompt [ssword:\s]: 
logout command [exit\r]: 
wakeup command [\r]: 
```

## Install Rules

Copy and paste the following rules and ruleset into the Local Manager.

```
config rule no F5info
conf rule F5info
description This rule runs failover show and collects the result into the F5ActiveInfo monitor variable
conditions
true
exit
action execute -command "b failover show" -pattern "FAILOVER (\D\D\D\D\D\D)" -setValue monitor F5ActiveInfo $1 
exit


conf rule no F5info1
conf rule F5info1
conditions
compare-value monitor F5ActiveInfo = active
exit
action writeStatus "Active"
exit


conf rule no F5info2
conf rule F5info2
conditions
compare-value monitor F5ActiveInfo = standb
exit
action writeStatus "Standby"
exit


config rule no F5prime1
config rule F5prime1
conditions
NOT has-value monitor F5state AND
compare-value monitor F5ActiveInfo = active
exit
action setValue monitor F5state active
exit


config rule no F5prime2
config rule F5prime2
conditions
NOT has-value monitor F5state AND
compare-value monitor F5ActiveInfo = standb
exit
action setValue monitor F5state standb
exit


config rule no F5becameActive
config rule F5becameActive
conditions
compare-value monitor F5ActiveInfo = active AND
compare-value monitor F5state = standb
exit
action setValue monitor F5state active
action alarm GENERIC -a "F5 changed to ACTIVE"
exit


config rule no F5becameStandby
config rule F5becameStandby
conditions
compare-value monitor F5ActiveInfo = standb AND
compare-value monitor F5state = active
exit
action setValue monitor F5state standb
action alarm GENERIC -a "F5 changed to STANDBY"
exit


config ruleset F5infoRules
rules
F5info | F5info1 | F5info2 | F5prime1 | F5prime2 | F5becameActive | F5becameStandby
exit
exit
```

## Configure Monitor

Use the **config monitor** command to add a monitor and attach the newly created ruleset.


