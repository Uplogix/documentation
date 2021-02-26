<!-- 5.4 -->

Display RADIUS/TACACS configuration for authentication to the Uplogix Local Manager. Use the show authentication command to display authentication information for devices being managed by the system.  

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system authentication
```

# Usage 

```
[admin@UplogixLM]# show system authentication
Authentication type: local
Limit maximum concurrent sessions: false
Use strong passwords: false
Expire password: false
Number of invalid attempts before lockout: 0
```

# In the Uplogix web interface

**Administration > AAA Settings** - applies to the entire inventory

**Inventory > group page > Security > Authentication** - specific to this inventory group

**Inventory > Local Manager page > Security > Authentication** - specific to this system

# History 

3.4 - This command was introduced to replace show Local Manager authentication.

# Related commands 

- **config system authentication**
- **config authentication**
- **show authentication**
