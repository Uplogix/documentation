<!-- 5.4 -->

Displays the Uplogix Local Managerâ€™s Reverse SSH tunnel status. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system reverse-ssh
```

# Usage 

```
[admin@UplogixLM]# show system reverse-ssh
Enabled: true
Limit SSH login to RSSH only: no
Reverse SSH server port: 2222
SSH keep-alive seconds: 90
SSH keep-alive bytes: 32

Remote: 198.51.100.1:2222
Active: 47 minutes, 53 seconds
Local: 198.51.100.48:36169 (47:53)

```

# In the Uplogix web interface

**Inventory > group page > Network > Reverse SSH** - specific to this inventory group

**Inventory > Local Manager page > Network > Reverse SSH** - specific to this system

#Related commands 

- **config system reverse-ssh**