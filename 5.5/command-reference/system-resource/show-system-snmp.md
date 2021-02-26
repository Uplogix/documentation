<!-- 5.4 -->

Command to display current SNMP information.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system snmp
```

# Usage 

```
[admin@xUplogix]# show system snmp
Security Level: authPriv
Port: 161
Username: xyzcoAus01
Auth Protocol: SHA
Auth Password: ********
Priv Protocol: AES256
Priv Password: ********
```

# In the Uplogix web interface

**Inventory > group page > Network > SNMP** - specific to this inventory group

**Inventory > Local Manager page > Network > SNMP** - specific to this system

# History

3.4 - This command was introduced to replace show Local Manager snmp.

# Related commands 

- **config system snmp**
