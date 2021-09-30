You can configure the Local Manager to monitor its network interfaces and alarm if the network connection goes down. This is often useful in bonding situations where removing one network cable doesn't necessarily affect connectivity.

Monitoring is disabled by default, but can be enabled with the **[config environment](/docs/local-manager-user-guide/system-configuration/environmental-thresholds)** command.

# Problem

The following alarms may be generated:

```
[super@UplogixLM]# show alarm
CDT   Elapsed Device Context Message                                                                
----- ------- ------ ------- -----------------------------------------------------------------------
04:40 0:30                    Primary network interface is down.     
04:40 0:30                    Secondary network interface is down.     
04:40 0:30                    Tertiary network interface is down.     
```

# Solution

This alarm can be corrected by resolving the connectivity issue with the affected network interface. Check cabling and switchport configuration.


If the alarm was generated in error, turn off monitoring of network interfaces that are not in use.

### From the Command Line:

Use the command **config environment** and set the Ethernet link failure to 'false' [n] on the unused network interfaces you're getting the alarm on (secondary Ethernet link in the below example). 

```
[admin@UplogixLM]# config environment
--- Existing  Values ---
Humidity Threshold: 75.0
Temperature Threshold: 99.0
Use Celsius: false
Alarm on power supply failure: true
Alarm on primary Ethernet link failure: true
Alarm on secondary Ethernet link failure: true
Alarm on tertiary Ethernet link failure: true
Change these? (y/n) [n]: y
--- Enter New Values ---
Humidity Threshold [75.0]: 
Temperature Threshold [99.0]: 
Use Celsius (y/n) [n]: 
Alarm on power supply failure (y/n) [y]: n
Alarm on primary Ethernet link failure (y/n) [y]: y
Alarm on secondary Ethernet link failure (y/n) [y]: n
Alarm on tertiary Ethernet link failure (y/n) [y]: n
Do you want to commit these changes? (y/n): y
```

### From the Control Center:

If you're seeing this alarm on multiple appliances, you can mass update on the group level by going to the inventory group on the UCC and navigating to **System** -> **Environment**. Uncheck the box next to the network interface(s) you're seeing the alarm on. Check the "force update on children" box next to the save button to apply the changes to appliances in any subgroups.     

![](http://i.imgur.com/Y8J6PzD.jpg)

> Some customers use only the primary network interface, but the primary and secondary interfaces are bonded by default. In this case, an alarm for the secondary or tertiary (if present) interfaces wouldn't be useful.