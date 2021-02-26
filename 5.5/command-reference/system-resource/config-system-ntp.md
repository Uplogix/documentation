<!-- 5.4 -->

Interactive command to enable NTP and direct Network Time Protocol requests to a time server, if the system is not configured to collect NTP from the Uplogix Control Center. 

If NTP is disabled, the internal clock will be used to set the system time. 

The Uplogix Local Manager does not provide NTP synchronization services to other devices.

> **Note**: If you configure the Uplogix Local Manager to be managed by an Uplogix Control Center, the system is automatically configured to use the Uplogix Control Center as an NTP server. You may change this manually; however, if the system time and the Uplogix Control Center time differ by more than a few seconds, this generates an error message. If you receive this alarm, set the Uplogix Control Center as the NTP primary server, or set both the Uplogix Control Center and the Local Manager to use the same NTP server.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system ntp
```

# Usage 

```
[admin@UplogixLM]# config system ntp
--- Existing  Values ---
Use NTP: yes
NTP Primary Server Hostname or IP: 198.51.238.20
NTP Secondary Server Hostname or IP: null
Change these? (y/n) [n]: y
--- Enter New Values ---
Use NTP:  (y/n) [y]:
NTP Primary Server Hostname or IP: [198.51.238.20]:
NTP Secondary Server Hostname or IP: []: 198.51.237.16
Do you want to commit these changes? (y/n): y
```

# In the Uplogix web interface

**Inventory > group page > Network > NTP** - specific to this inventory group

**Inventory > Local Manager page > Network > NTP** - specific to this 
system

# History 

3.4 - This command was introduced to replace config Local Manager ntp.

# Related commands 

- **show system ntp**
- **config system management**
- **config date**
