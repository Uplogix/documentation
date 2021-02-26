<!-- 5.5.3 -->

This service switch ruleset uses pings to a specified target to trigger a routing change on a managed Cisco device. 


To load the rules onto the Uplogix LM, connect to the command line at the system level and enter the following:


```
config rule no pingServiceSwitchprime
config rule pingServiceSwitchprime
action setValue system ServiceSwitchState 0
conditions
NOT has-value system ServiceSwitchState 
exit
exit


config rule no pingServiceSwitchPingLog
config rule pingServiceSwitchPingLog
action event GENERIC -a "ping failed"
conditions
ping.roundTripTime equals 0
exit
exit


config rule no pingServiceSwitchon
config rule pingServiceSwitchon
action event GENERIC -a "ping failed - turning ServiceSwitch on"
action setValue system ServiceSwitchState 1
action execute -raw -pattern "#" -command "ROUTER COMMANDS GO HERE"
conditions
ping.roundTripTime equals 0 :3i AND
compare-value system ServiceSwitchState = 0 
exit
exit


config rule no pingServiceSwitchoff
config rule pingServiceSwitchoff
action event GENERIC -a "ping succeeded - turning ServiceSwitch off"
action setValue system ServiceSwitchState 0
action execute -raw -pattern "#" -command "ROUTER COMMANDS GO HERE"
conditions
NOT ping.roundTripTime equals 0 :100i AND
compare-value system ServiceSwitchState = 1
exit
exit
```
 
To schedule the monitor and rules, navigate to the port with the Cisco device and enter the following, replacing 10.10.10.1 with the IP address the Cisco will be pinging to:

```
config monitor ping 10.10.10.1 pingServiceSwitchprime | pingServiceSwitchPingLog | pingServiceSwitchon | pingServiceSwitchoff :5
```