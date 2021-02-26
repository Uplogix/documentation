<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary >Â System > Environment</div>

All models of the Local Manager, except the 430, can measure temperature and humidity, providing constant and reliable environmental monitoring. The 500, 3200, and 5000 Local Managers require an optional temperature and humidity probe.

The default temperature limit for Local Managers with sensing capability is 95Â° F (35Â° C), and the default humidity limit is 85%. If the temperature or humidity exceeds the defined threshold, an alarm is triggered. Alarms are not triggered if the relevant data is unavailableâ€”for example, if no sensor is installed.

In addition to temperature and humidity, the environment settings allow you to specify which hardware resources are connected so that the Local Manager can report a failure/alarm when one exists. This includes indicators for all Ethernet interfaces and an indicator to alarm on power supply failure (for example, when both power supplies are connected on the Uplogix 5000).

All of these settings can be changed using the **config environment** command as shown below.

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