<div class='ucc' />Inventory > Local Manager Summary > System > Environment</div>

Uplogix Local Managers can monitor temperature and humidity via an optional environmental sensor probe.

The default temperature threshold for Local Managers with sensing capability is 95° F (35° C), and the default humidity threshold is 85%. If the temperature or humidity exceeds the defined threshold, an alarm is triggered. **Alarms are not triggered if the relevant data is unavailable**—for example, if no sensor is installed.

> The values listed here are recommended thresholds. The actual environmental operating limits will vary per hardware model.

Environmental thresholds can be changed using the **config environment** command as shown below.

```
[admin@UplogixLM]# config environment
--- Existing  Values ---
Humidity Threshold: 85.0
Temperature Threshold: 95.0
Use Celsius: false
Alarm on power supply failure: false
Alarm on primary Ethernet link failure: false
Alarm on secondary Ethernet link failure: false
Alarm on tertiary Ethernet link failure: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Humidity Threshold [85.0]: 
Temperature Threshold [95.0]: 40
Use Celsius (y/n) [n]: y
Alarm on power supply failure (y/n) [n]: y
Alarm on primary Ethernet link failure (y/n) [n]: y
Alarm on secondary Ethernet link failure (y/n) [n]:
Alarm on tertiary Ethernet link failure (y/n) [n]:
Do you want to commit these changes? (y/n): y
```

To view the current environmental readings, use the **show environment** command.

```
[admin@UplogixLM]# show environment
Current temperature: 77.46 degrees F
Current humidity:    38.72%
Average temperature over the last hour: 80.22 degrees F
Average humidity over the last hour:    38.16%
Power supply status: Power 2 inactive
Primary Ethernet status:   Link up
Secondary Ethernet status: Link down ; interface down
Tertiary Ethernet status:  Not Installed
```

# Hardware Alarms
Integrated power supplies and Ethernet link statuses are included in the Local Manager's environmental monitoring.

Alarms for power and Ethernet failures are disabled by default. To enable alarms, use the **config environment** command.

```
[admin@UplogixLM]# config environment
--- Existing  Values ---
Humidity Threshold: 85.0
Temperature Threshold: 95.0
Use Celsius: false
Alarm on power supply failure: false
Alarm on primary Ethernet link failure: false
Alarm on secondary Ethernet link failure: false
Alarm on tertiary Ethernet link failure: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Humidity Threshold [85.0]: 
Temperature Threshold [95.0]: 
Use Celsius (y/n) [n]: 
Alarm on power supply failure (y/n) [n]: y
Alarm on primary Ethernet link failure (y/n) [n]: y
Alarm on secondary Ethernet link failure (y/n) [n]: y
Alarm on tertiary Ethernet link failure (y/n) [n]: y
Do you want to commit these changes? (y/n): y
```

If power supplies or Ethernet interfaces are disconnected, an alarm will be generated.

```
[admin@UplogixLM]# show alarms
CDT       Elapsed     Device     Context     Message                                                    
-----     -------     ------     -------     -----------------------------------------------------------
09:40     0:11                                Power lost. (Power 2)                                     
09:40     0:11                                Secondary network interface is down.                      
```