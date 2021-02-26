This ruleset is designed to detect which of a set of Cisco ASAs are active and which is on standby. In addition, when either changes from primary to secondary or vice versa an email alarm will be sent indicating such.

To load these rules on your Uplogix LM, copy and paste the below rules and rulesets into the CLI on the system resource.

To schedule the monitors, on the primary ASA's port run the command **config monitor chassis fsd1**, and on the secondary ASA's port run the command **config monitor chassis fsd2**.

```
config rule no fsdPrime1
config rule fsdPrime1
conditions
NOT has-value monitor 1wasActive 
exit
action setValue monitor 1wasActive 1
exit

config rule no fsdPrime2
config rule fsdPrime2
conditions
NOT has-value monitor 2wasActive 
exit
action setValue monitor 2wasActive 0
exit

config rule no fsd1Check
config rule fsd1Check
conditions
true
exit
action execute -command "show failover | include This host" -pattern "This host: Primary - (\D\D\D\D\D\D)" -setValue monitor fsd1Response $1 
exit

config rule no fsd2Check
config rule fsd2Check
conditions
true
exit
action execute -command "show failover | include This host" -pattern "This host: Secondary - (\D\D\D\D\D\D)" -setValue monitor fsd2Response $1 
exit

config rule no fsdMatch1
config rule fsdMatch1
conditions
compare-value monitor fsd1Response = Active
exit
action clearValue monitor fsd1Response
action writeStatus "Active"
action setValue monitor 1active 1
exit

config rule no fsdMatch2
config rule fsdMatch2
conditions
compare-value monitor fsd1Response = Standb
exit
action clearValue monitor fsd1Response
action writeStatus "Standby"
action setValue monitor 1active 0
exit

config rule no fsdMatch3
config rule fsdMatch3
conditions
compare-value monitor fsd2Response = Active
exit
action clearValue monitor fsd2Response
action writeStatus "Active"
action setValue monitor 2active 1
exit

config rule no fsdMatch4
config rule fsdMatch4
conditions
compare-value monitor fsd2Response = Standb
exit
action clearValue monitor fsd2Response
action writeStatus "Standby"
action setValue monitor 2active 0
exit

config rule no fsdAlert1
config rule fsdAlert1
conditions
compare-value monitor 1active = 1 AND
compare-value monitor 1wasActive = 0
exit
action alarm GENERIC -a "Primary became active"
action setValue monitor 1wasActive = 1
exit

config rule no fsdAlert2
config rule fsdAlert2
conditions
compare-value monitor 1active = 0 AND
compare-value monitor 1wasActive = 1
exit
action alarm GENERIC -a "Primary went to standby"
action setValue monitor 1wasActive = 0
exit

config rule no fsdAlert3
config rule fsdAlert3
conditions
compare-value monitor 2active = 1 AND
compare-value monitor 2wasActive = 0
exit
action alarm GENERIC -a "Secondary became active"
action setValue monitor 2wasActive = 1
exit

config rule no fsdAlert4
config rule fsdAlert4
conditions
compare-value monitor 2active = 0 AND
compare-value monitor 2wasActive = 1
exit
action alarm GENERIC -a "Secondary went to standby"
action setValue monitor 2wasActive = 0
exit

config ruleset no fsd1
config ruleset fsd1
rules
fsdPrime1 | fsd1Check | fsdMatch1 | fsdMatch2 | fsdAlert1 | fsdAlert2
exit
exit

config ruleset no fsd2
config ruleset fsd2
rules
fsdPrime2 | fsd2Check | fsdMatch3 | fsdMatch4 | fsdAlert3 | fsdAlert4
exit
exit
```