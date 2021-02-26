<!-- 5.4 -->

Interactive command to specify the details for forwarding the Uplogix Local Manager's logs to a syslog server.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system syslog-options
```

# Usage 

```
[admin@UplogixLM]# config system syslog-options
--- Existing  Values ---
Syslog enabled: no
Syslog server IP: 
Syslog port number: 514
Syslog facility: 
Change these? (y/n) [n]: y
--- Enter New Values ---
Enable syslog? (y/n) [n]: y
Syslog server IP: []: 198.51.235.91
Syslog port number: [514]: 
Syslog facility: []: local5
Do you want to commit these changes? (y/n): y
```

# In the Uplogix web interface

**Inventory > group page > Network > Syslog** - specific to this inventory group

**Inventory > local Manager page > Network > Syslog** - specific to this system

# History 

3.4 This command was introduced.

# Related commands 

- **show system syslog-options**
