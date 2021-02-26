<!-- 5.4 -->

Interactive command that steps you through the changes needed to update or set the credentials used to communicate with a network device. To set up authentication for the Uplogix Local Manager, use the **config system authentication** command.

# Command availability 

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, ppp, server

Secondary authentication available on Cisco IOS, Pix, ASA and CatIOS

Power controllers: APC, BayTech, Server Technology

Uplogix system: All

LMS offerings: All

# Syntax 

```
config authentication
```

# Usage 

```
[admin@UplogixLM (port1/3)]# config authentication
--- Existing  Values ---

console user: tasman
console password: ********
enable user:
enable password: 
secondary console username:
secondary console password: ********
secondary enable username:
secondary enable password: ********
Change these? (y/n) [n]: y
--- Enter New Values ---
console username: [tasman]:
console password [*********]:*****
confirm password:*****
enable username: []:
enable password []:
secondary console username:
secondary console password: ********
secondary enable username:
secondary enable password: ********
Would you like to test the supplied values? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
Saving credentials.
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all devices that match the selected filter

**Inventory > Local Manager page > port detail > schedule button** - specific to this device

# History 

--

# Related commands 

- **config init**
- **config system authentication**
- **show authentication**
- **show system authentication**
- **rollback authentication**
- **clear password**
