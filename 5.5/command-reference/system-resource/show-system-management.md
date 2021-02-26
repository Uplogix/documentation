<!-- 5.4 -->

Displays the Uplogix Control Center configuration.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax

```
show system management
```

# Usage

```
[admin@UplogixLM]# show system management
Use Management Server: yes
Hostname or IP: 198.51.238.20
Port: 8443
Heartbeat interval (seconds): 30
Heartbeat band: all
Always use minimal heartbeat: false
Last successful heartbeat: 10/13/2017 18:48:36 GMT (Full)

```

# In the Uplogix web interface

**Inventory > group page> Network > Management Server** - specific to this inventory group

**Inventory > Local Manager page > Network > Management Server** - specific to this system

# History 

3.4 - This command was introduced to replace show Control Center.

# Related commands 

- **config system management**
