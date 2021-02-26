<!-- 5.4 -->

Interactive command to set the alarm threshold for ambient temperature (32-port Uplogix Local Managers) or for temperature and humidity (older 4-port Uplogix Local Managers). This command is not available for the Uplogix 430, 500, or  5000 Local Manager.

# Command availability 

CLI resource: system

Uplogix system: 3200, 400

LMS offerings: All

# Syntax 

```
config environment
```

# Usage 

32-port Uplogix Local Managers ship with an external 1-WireÂ® temperature sensor; older 4-port Local Managers have a temperature and humidity sensor built in. 

Exceeding temperature or humidity thresholds (if applicable) will trigger alarms. If environmental data is unavailable - for example, if the sensor has not been connected - the corresponding alarm(s) will not be triggered.

```
[admin@UplogixLM]# config environment
--- Existing  Values ---
Humidity Threshold: 85.0
Temperature Threshold: 95.0
Use Celsius: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Humidity Threshold: [85.0]: 75
Temperature Threshold: [95.0]: 99
Use Celsius: (y/n) [n]: n
Do you want to commit these changes? (y/n): y
```

# History 

--

# Related commands 
 
- **show environment**
