# Problem

The following alarm occurs:

```
[admin@sup101]# show alarm
 CDT       Elapsed     Device     Interface     Message                                   
 -----     -------     ------     ---------     -------------------------------------------
 10:00     1:24                                  USB serial device disconnected from envoy.
``` 

# Symptoms

When this alarm is active, some or all of the ports may be inaccessible. Additionally, the dashboard may show some or all ports as UNAVAILABLE.

```
[admin@sup101]# show dashboard
 ------------------------------------------------------------------------------
 Port     Hostname            Status        Con Eth Uptime   Processor   Last
                                                            Utilization  Alarm
 ---- ------------------ ------------------ --- --- ------- ----------- -------
  1/1                    OK                                                   
  1/2                                                                         
  1/3                                                                         
  1/4                                                                         
  1/5                    UNAVAILABLE      
  1/6                    UNAVAILABLE      
  1/7                    UNAVAILABLE       
  1/8                    UNAVAILABLE      
  PWR ServerTech                                                              
  MDM iridium            OK                  *                          9d 18h
    E sup101             OK                      *           00/02/06   2m 58s
 ------------------------------------------------------------------------------
 Con(sole) or Eth(ernet) link status indicated with '*'
 Processor Utilization displayed as last collected, 1 and 5 minute averages
 Last Alarm displays time since last Alarm matched.
                   d=day, h=hour, m=minute, s=second
```

# Solution

This alarm usually indicates that an option card (3200) or expansion box (400) has been removed from the appliance. If no devices have been removed, this could also indicate a communication problem with the option card or expansion box.

Shut down your appliance with the **shutdown** command or from the front panel.
If the option card or expansion box is still attached, carefully remove it from the appliance. Option cards have two thumb screws on the front that need to be loosened.

Reinstall the option card and tighten thumb screws.

Power the appliance on and check alarms.

If these steps do not resolve the issue, please contact Uplogix Support for further troubleshooting steps.