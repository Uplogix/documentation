<!-- 5.4 -->

The following rule is designed to monitor an iDirect to see if Falcon is running, and if not, to push the last saved startup config to the iDirect.

```
config rule iDirectFalconNotRunning
conditions
chassis.boolean1 equals false 4i AND
NOT has-run pushStartupConfig :15m
exit
action pushStartupConfig current
action alarm GENERIC -a "Falcon not running - pushing startup config"
exit
```

To implement the rule, go to the iDirect's port and schedule a chassis monitor with that rule attached with the following command:

```
config monitor chassis iDirectFalconNotRunning
```