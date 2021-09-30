<!-- 5.4 -->

Assimilate modifies the network device to work efficiently with the Uplogix Local Manager. Changes vary by device, but can include console speed, logging, and authentication.

# Command availability 

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Foundry, GE, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sea Tel, Spacetrack, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
assimilate
```

# Usage 

**assimilate** will make changes based on settings configured for this type of device. This command is automatically called during **config init** to optimize the Local Manager's interaction. 

```
[admin@UplogixLM (port1/1)]# assimilate
Setting buffered logging.
Setting configured speed to 19200.
Setting logging synchronous.
```

# History 
--

# Related commands 

* **rollback assimilate**
* **config init**