<!-- 5.4 -->

Displays settings for collection of a deviceâ€™s log.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show device logging
```

# Usage 

```
[admin@uplogixLM (port1/1)]# show device logging
Set the console to use synchronous logging: yes
Set the console to use logging buffered: yes
Device buffer polling interval: 30
Clear device log buffer on poll: yes
Port syslog forwarding enabled: no
Syslog server IP:
Syslog port number: 514
Syslog facility:
```

# History 

1.04 - syslog forwarding parameters were added.

2.0 - Changed from show logging to show device logging

# Related commands 

- **config device logging**
- **show device syslog**
