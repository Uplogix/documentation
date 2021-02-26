<!-- 5.4 -->

Displays the current syslog retrieved from the device. The last 20 currently available parsed console messages are displayed.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, 
Nortel, Sun, Tasman, server

Uplogix Local Managers: All****

LMS offerings: All

# Syntax 

```
show device syslog [-n <"number">]
```
-n <"number"> - number of lines

#Usage 
Like the interface statistics and system logs, the device syslog messages are rolled off to either archive or export hosts and only the current logs are displayed. The default interval for the roll-off is 60 minutes.

```
[admin@UplogixLM (port1/3)]# show device syslog
07/26/08 17:09:01.498 5 ETHC PORTTOSTP Port 2/3 joined bridge port 2/3
07/26/08 17:09:01.484 5 ETHC PORTTOSTP Port 2/2 joined bridge port 2/2
07/26/08 17:09:01.469 5 ETHC PORTTOSTP Port 2/1 joined bridge port 2/1
07/26/08 17:09:01.455 5 SYS MOD_OK Module 2 is online
07/26/08 17:07:50.891 5 SYS MOD_OK Module 1 is online
07/26/08 17:07:50.868 2 SYS PS_NFANFAIL Power supply 1 failed
```

# In the Uplogix web interface

**Inventory > Local Manager page > port detail > Syslog**

# History 

2.0 - This command replaced show syslog.

# Related commands 

- **show device logging**
