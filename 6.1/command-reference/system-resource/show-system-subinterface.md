<!-- 5.4 -->

Display subinterface configuration

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system subinterface <name | *>
```

# Usage 

```
[admin@UplogixLM]# show system subinterface Voice
name Voice
vlan 30
ip 192.0.23.1/24
gateway 192.0.23.254
route 192.0.24.0/24
```

# In the Uplogix web interface

**Inventory > Local Manager page > Network > Subinterfaces** - specific to this system

# History 

4.4 - This command was introduced.

# Related commands 

- **config system subinterface**
- **show system route**
