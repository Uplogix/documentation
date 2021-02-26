<!-- 5.4 -->

Allows you to set a DHCP base address that the Uplogix Local Manager uses in assigning DHCP addresses to connected devices. Port devices may be configured to acquire DHCP addresses from the system as a part of the config init dialog. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system protocols dhcp <base DHCP address>
```

# Usage 
The base DHCP address parameter is the base address to be used in generating DHCP addresses for connected devices. The default base address is 169.254.100.

```
[admin@UplogixLM]# config system protocols dhcp 169.254.100
```

> **Note**: When setting the Local Manager to assign DHCP addresses to devices, the DHCP pool must not overlap with other pools or subnets. The base address must not overlap the system's management IP address or existing static assignments on ports.

# In the Uplogix web interface

**Inventory > group page > Network > Protocols > DHCP Settings** - specific to this inventory group

**Inventory > Local Manager page > Network > Protocols > DHCP Settings** - specific to this system

# History 

3.4 - This command was introduced.

# Related commands

- **show system protocols**
