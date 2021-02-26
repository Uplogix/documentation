<!-- 5.4 -->

Displays scheduled jobs for the network device.

# Command availability

CLI resource: system, port

Device makes: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show schedules
```

# Usage

The frequency and internal command are displayed.

```
[admin@UplogixLM (port1/3)]# show schedules
Listing currently scheduled jobs for device: port3
0: [Interval: 00:05:00 Mask: * * * * *]deviceInfo
1: [Interval: 03:00:00 Mask: * * * * *]pullConfig running-
2: [Interval: 24:00:00 Mask: * * * * *]pullConfig startup-
3: [Interval: 336:00:00 Mask: * * * * *]pullOS
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > Local Manager page > Scheduled Tasks** - specific to this system


# History 
--

# Related commands 

**config schedule**
**config removejob**
