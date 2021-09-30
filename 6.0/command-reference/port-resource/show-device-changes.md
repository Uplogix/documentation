<!-- 5.4 -->

Displays a summary of changes to a device. The list can be filtered by user ID. To see detailed information about a change, use the **show device change** command.

# Command availability
CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show device changes ["userID"]
```

Use the optional userID parameter to view changes made by a specific user.

# Usage 

```
[admin@UplogixLM (port 2/1)]# show device changes  
id        user      ip address         changed         
-----     -----     --------------     ----------------
98305     ksmith     156.38.66.1     Feb 15 06:46 UTC
61233     djones     156.38.125.55   Jan 31 10:46 UTC
98305     secadm     156.38.100.2    Jan 30 06:00 UTC
98305     ksmith     156.38.66.1     Jan 16 18:46 UTC
```

# In the Uplogix web interface

**Inventory > Local Manager page > port detail > Changes**  

#History 

1.4 - This command was introduced.

# Related commands 

- **show device change**
