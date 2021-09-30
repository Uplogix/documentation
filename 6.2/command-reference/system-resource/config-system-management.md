<!-- 5.4 -->

Interactive command to associate the Uplogix Local Manager with an Uplogix Control Center. The heartbeat uses between 1 and 20 kilobytes for communication.  This command additionally sets NTP to use the server's address.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All
# Syntax

```
config system management
```

# Usage

```
[admin@UplogixLM]# config system management
--- Existing  Values ---
Use  Management Server: n
Hostname or IP: 127.0.0.1
Port: 8443
Heartbeat interval (seconds): 30
Heartbeat band: all
Last successful heartbeat:  (not yet contacted)
Change these? (y/n) [n]: y
--- Enter New Values ---
Use Management Server (y/n/auto) [n]: y
Hostname or IP: [127.0.0.1]: 198.51.51.20
Set ntp location to 198.51.51.20: (y/n) [y]:
Port: [8443]:
Heartbeat interval (seconds): [30]:
Heartbeat during: [all]:
Do you want to commit these changes? (y/n): y
```

Heartbeat during specifies when the Uplogix Local Manager provides a heartbeat, and may be set to inband, outband, or all.

Minimal heartbeat can be configured from the UCC.  The setting is displayed as:

```
Always use minimal heartbeat: true
```

You will only be prompted for the NTP location if the Local Manager has not been managed by an Uplogix Control Center before. 

> **Note**: If the Local Manager has been managed by the Uplogix Control Center at some time in the past, this command will not configure NTP. In this situation, use the **config system ntp** command to set the Uplogix Control Center as the Local Manager's NTP server. 

# In the Uplogix web interface

**Inventory > group page> Network > Management Server** - specific to this inventory group

**Inventory > Local Manager page > Network > Mangement Server** - specific to this system

# History 

3.4 - This command was introduced  

4.5  - Minimal Heartbeat option (display only)

# Related commands 

- **show system management**
- **config system ntp**
- **config system archive**
