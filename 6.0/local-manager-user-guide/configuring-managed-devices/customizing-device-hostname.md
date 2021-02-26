# Overview

The hostname of each managed device is used in the dashboard view that is displayed when logging in or when using the **show dashboard** command. If no hostname is available, the description is used.

```
[admin@UplogixLM]# show dashboard
------------------------------------------------------------------------------
Port     Hostname            Status        Con Eth Uptime   Processor   Last 
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
 1/1 AUS-CORE           OK                  *   *  11m 35s    00/00/00 26s    
 1/2                                            -                             
 1/3                                            -                             
 1/4                                            -                             
 1/5                                            -                             
 1/6                                            -                             
 1/7                                            -                             
 1/8                                            -                             
 MDM embedded           none                                                  
 SYS UplogixLM          OK                      *  23h 52m    02/02/03 6s     
------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
                  d=day, h=hour, m=minute, s=second

Ports 1/1-1/8 have dedicated Ethernet.
```

If the Local Manager has a front panel display, it will scroll the hostname and status for each managed device.

# Configure Displayed Hostname

To change the description of a port, use the **config info** command. This is useful for ports in native mode.

```
[admin@UplogixLM (port1/2)]# config info
Description: 
Make: native
Management IP: 
Change these? (y/n) [n]: y
--- Enter New Values ---
description: DAL-CORE Primary Router
make [native]: 
management IP: 
Configure dedicated Ethernet port? (y/n) [n]: 
Do you want to commit these changes? (y/n): y
Description: DAL-CORE Primary Router
Make: native
Management IP: 
```

Since no hostname is available on a native port, the description will be displayed in the dashboard.

```
[admin@UplogixLM (port1/2)]# show dash
------------------------------------------------------------------------------
Port     Hostname            Status        Con Eth Uptime   Processor   Last 
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
 1/2 DAL-CORE Primary R                         -                             
------------------------------------------------------------------------------
```