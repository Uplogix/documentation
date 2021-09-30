<!-- 5.4 -->

Displays a device's make, model, OS, and other information. The information collected and displayed depends on what is configured on the resource. This command displays a subset of the information available from the **show all** command.

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: All

Modem: All

Power controllers: All

Uplogix system: All

LMS offerings: All

# Syntax 

```
show info
```

# Usage 
The information displayed varies; the following is a representative example for a managed device.

```
[admin@UplogixLM (port1/1)]# show info
Hostname: Cat4003
Description: 86012222-rms235
Make: cisco
Model: WS-C4003
OS: CatOS
OS Version: 7.6(7)
Management IP: 198.51.235.11
Current CPU Utilization: 0.0%
CPU Utilization (1 minute average): 7.8%
CPU Utilization (5 minute average): 6.3%
Total Memory: 54049576 bytes
Used Memory: 4179536 bytes
Free Memory: 49870040 bytes
```

# History 

1.1 - Memory and CPU utilization was added. 

# Related commands 
- 
- **show status**
- **show all**
- **config info**
