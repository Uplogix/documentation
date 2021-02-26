<!-- 5.4 -->

Displays the parameters used to send the Uplogix Local Managerâ€™s own logs to a syslog server.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system syslog-options
```

# Usage 

```
[admin@UplogixLM]# show system syslog-options
Syslog enabled: yes
Syslog server IP: 198.51.235.91
Syslog port number: 514
Syslog facility: local5
```

# In the Uplogix web interface

**Inventory > group page > Network > Syslog** - specific to this inventory group

**Inventory > Local Manager page > Network > Syslog** - specific to this system

# History 

3.4 - This command was introduced to replace show Local Manager syslog-options.

# Related commands 

- **config system syslog-options**
