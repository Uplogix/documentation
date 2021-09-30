<!-- 5.4 -->

Displays the transactional rollback contents that would be applied to the device's running configuration if the rollback config command were called.

# Command availability 

CLI resource: port

Device makes: Alcatel, Cisco, Comtech EF Data, Garmin, iDirect, Juniper, Netscreen, Sun, Tasman, ppp

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show rollback-config [candidate | current | previous | archive #]
```

# Usage 

```
[admin@UplogixLM (port 1/4)]# show rollback-config
!
router ospf 100
 no network 198.51.254.16 0.0.0.3 area 20
 network 198.51.254.16 0.0.0.3 area 25
!
```

# In the Uplogix web interface

**Inventory > Local Manager page > port detail > Files** - specific to this device

# History 
--

# Related commands 

- **rollback config**
