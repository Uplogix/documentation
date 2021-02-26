Interactive command to set the alarm threshold for ambient temperature (32-port Uplogix Local Managers) or for temperature and humidity (older 4-port Uplogix Local Managers). This command is not available for the Uplogix 430, 500, or  5000 Local Manager.

This command configures alarm thresholds for temperature and humidity as observed by a Local Manager. It also enables and disables alarms for power and physical Ethernet connectivity loss.

> Temperature and humidity monitoring is available via an add-on module on modern Local Managers.

# Command availability 

CLI resource: system

Uplogix system: Local Manager equipped with a temperature / humidity sensor (for temperature / humidity monitoring)

LMS offerings: All

# Syntax 

```
config environment
```

# Usage 

Exceeding temperature or humidity thresholds (if applicable) will trigger alarms. If environmental data is unavailable - for example, if the sensor has not been connected - the corresponding alarm(s) will not be triggered.

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
Humidity Threshold [85.0]: 75
Temperature Threshold [95.0]: 99
Use Celsius (y/n) [n]: 
Alarm on power supply failure (y/n) [n]: y
Alarm on primary Ethernet link failure (y/n) [n]: y
Alarm on secondary Ethernet link failure (y/n) [n]: y
Alarm on tertiary Ethernet link failure (y/n) [n]: y
Do you want to commit these changes? (y/n): y
```

# History 

--

# Related commands 
 
- **show environment**
