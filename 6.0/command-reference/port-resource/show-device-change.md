<!-- 5.4 -->

Display net changes to a device after a pass-through operation. Use the **show device changes** command first to display a list of changes; then use the **show device change** command to view information about the change of interest. 

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show device change <"ID #">
```

The ID # parameter is the change identification number listed for this change in the show device changes command.

# Usage 

Changes that represent additions are prefixed with **+**; changes that represent deletions are 
prefixed with **-**. Other lines included for context.

```
[admin@UplogixLM (port 2/1)]# show device change 9541 
------------------------------------------------------------
User: djones
From: 156.30.1.22
Changed: Jul 15 06:46:02 UTC 2017
Comment:
------------------------------------------------------------
router bgp 100
+neighbor 180.10.30.4 remote-as 3498
------------------------------------------------------------
--DONE--
```

# History 

1.4 - This command was introduced.
3.2 - Added Comment field.

# Related commands 

- **show device changes**
