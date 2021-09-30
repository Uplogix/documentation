<!-- 5.4 -->

Interactive command to provision 802.1Q tagged interfaces on the Uplogix management interface.  Named subinterfaces are associated with VLAN id, IP addresses and gateways, and specific IP routes directed through its gateway.

Standard switch configuration should be trunk mode with native VLAN set for Local Manger "Management" IP address.  

Routes set override default routes but are overridden by static routes set on the management IP address.
 
# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system subinterface <name>
```

# Usage 

```
[admin@UplogixLM]# config system subinterface Voice
Subinterface Voice does not exist. Create (y/n): y
Warning: Remote connections may be lost if you commit changes.
[config subint Voice]# vlan 30
[config subint Voice]# ip 192.0.23.1/24
[config subint Voice]# gateway 192.0.23.254
[config subint Voice]# route 192.0.24.0/24
[config subint Voice]# exit
```

> **Note**: Networking will be restarted after configuration of subinterfaces. 

# In the Uplogix web interface

**Inventory > Local Manager page > Network > Subinterfaces** - specific to this system

# History 

4.4 - This command was introduced.

#Related commands 

- **show system subinterface**
- **show system route**
