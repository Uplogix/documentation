<!-- 5.4 -->

This ruleset monitors the signal level of the Ubiquiti and triggers the shutdown of an interface on a router when the level goes below -75 for three consecutive checks. When the signal level is above -75 db for three consecutive checks the router's interface is turned on again.

# Usage

First, replace INTERFACE-NAME-GOES-HERE in the ubiquitiRouterInterfaceOff and ubiquitiRouterInterfaceOn rules below with the name of the router interface to be controlled.

To load the rules, copy and paste the rules and rulesets into the system level of the Uplogix Local Manager's CLI.

To schedule the rules on the Ubiquiti, switch to the Ubiquiti's port with the **port 4/1** command and issue the command **config monitor chassis ubiquitiCheck**. Validate the monitor by pressing "y".

Finally, to schedule the rules on the router, switch to the Router's port and run the command **config monitor chassis ubiquitiRouterInterface**.

# Rules and Rulesets

```
config rule no ubiquiti
config rule ubiquiti
description gathers level quality into variable Ubiquiti2
conditions
true
exit
action execute -command "cat /proc/net/wireless | grep ath0 | sed -e 's/ */ /g' | cut -d' ' -f5 | sed s/[.]//" -pattern "(\d\d)" -setValue monitor Ubiquiti2 $1 
exit

config rule no ubiquiti1
config rule ubiquiti1
description
conditions
compare-value monitor Ubiquiti2 > 75
exit
action alarm GENERIC -a "level below -75 decibels"
action writeStatus Level Low
exit

config rule no ubiquiti2
config rule ubiquiti2
description
conditions
compare-value monitor Ubiquiti2 > 75 :3i
exit
action event GENERIC -a "Signal level low - triggering interface shutdown"
action setValue system UbiquitiSingnalLow 1
exit

config rule no ubiquiti3
config rule ubiquiti3
description
conditions
compare-value monitor Ubiquiti2 < 75 :3i
exit
action event GENERIC -a "Signal level above 75 - triggering interface on"
action setValue system UbiquitiSingnalLow 0
exit

config ruleset no ubiquitiCheck
config ruleset ubiquitiCheck
rules
ubiquiti | ubiquiti1 | ubiquiti2 | ubiquiti3
exit
exit

config rule no ubiquitiRouterInterfaceOff
config rule ubiquitiRouterInterfaceOff
conditions
compare-value monitor UbiquitiSingnalLow = 1
exit
action interfaceOff -i INTERFACE-NAME-GOES-HERE
exit

config rule no ubiquitiRouterInterfaceOn
config rule ubiquitiRouterInterfaceOn
conditions
compare-value monitor UbiquitiSingnalLow = 0 OR
NOT has-value system UbiquitiSingnalLow 
exit
action interfaceOn -i INTERFACE-NAME-GOES-HERE
exit

config ruleset no ubiquitiRouterInterface
config ruleset ubiquitiRouterInterface
rules
ubiquitiRouterInterfaceOff | ubiquitiRouterInterfaceOn
exit
exit
```