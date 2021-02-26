<!-- 5.4 -->

Displays the status of devices on each port.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show ports
```

# Usage 

The status column is blank if there are no current alarms.
```
[admin@UplogixLM]# show ports
Port         Host Name       Make    Model    OS             Status
----         ---------       ----    -----    --             ------
port1/1      tasman-6300-ds3 tasman  6300     TiOS r6        OK
port1/2      Austin_Netra    sun              solaris 5.10   OK
port1/3      Cat6009         cisco   WS-C6009 CatOS 7.6(7)   OK
port1/4                      native   
```

# In the Uplogix web interface

**Inventory > Local Manager page > Summary** - ports on this system

# History 
--

# Related commands 

- **show status**
