<!-- 5.4 -->

Interactive command to specify how logging is handled for the network device.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix system: All

LMS offerings: All

# Syntax 

```
config device logging
```

# Usage 

This setting may alter the network device's configuration, based on the user's choices at the next assimilation process.

This setting does not remove current syslog configuration from network devices.

```
[admin@UplogixLM (port1/1)]# config device logging 
--- Existing  Values ---
Set the console to use synchronous logging: yes
Set the console to use logging buffered: yes
Logging level for buffered logging (PIX only): 3
Device buffer polling interval: 30
Clear device log buffer on poll: no
Port syslog forwarding enabled: no
Change these? (y/n) [n]: y
Set the console to use synchronous logging: (y/n) [y]: y
Set the console to use logging buffered: (y/n) [y]: y
Logging level for buffered logging (PIX only): [3]:
Device buffer polling interval: [30]: 
Clear device log buffer on poll: (y/n) [y]: 
Enable syslog forwarding? (y/n) [n]: y
Syslog server IP: []: 198.51.235.244
Syslog port number: [514]: 
Syslog facility: []: local1
```

# In the Uplogix web interface

Console log and buffer settings: **Inventory > group page > System > Defaul Port Settings button** - specific to this inventory group

Syslog settings: **Inventory > Local Manager page > Port Settings > Logging** - specific to this device

# History 

2.0 - This command was introduced

# Related commands 

- **assimilate**
- **show device logging**
