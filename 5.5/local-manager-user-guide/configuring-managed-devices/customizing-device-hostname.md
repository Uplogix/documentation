<!-- 5.4 -->

The hostname of each port device is used in the dashboard view that is displayed when logging in or when using the **show dashboard** command. If no hostname is available, the description is used.

```
Uplogix LMS v5.4 30605 -- Powering Business Uptime
------------------------------------------------------------------------------
Port     Hostname            Status        Con Eth Uptime   Processor   Last 
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
 1/1 AUS-CORE           OK                 *                           42d 12m
 1/2 DAL-CORE           OK                 *                           42d 12m
 1/3 AUS-DMZ            OK                 *                           42d 12m
 1/4 Old Router         OK                                             42d 12m
 MDM Verizon LTE                                                                 
 SYS UplogixLM         OK                      *  53d 23h    07/07/07 41d 23h
------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
                  d=day, h=hour, m=minute, s=second
```

The front panel display on the Uplogix 5000 Local Manager also provides information including the hostname and status for each port device. The hostname may be what the Local Manager retrieves from the device or what you set as the description.

To change the description of a port, use the **config info** command.