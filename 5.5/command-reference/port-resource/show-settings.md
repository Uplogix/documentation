<!-- 5.4 -->

Displays the settings for the device.

# Command availability 

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Enhanced, Foundry, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show settings
```

# Usage 

```
[admin@uplogixLM (port1/1)]# show settings
1 Assimilated terminal speed: 19200
2 Modify terminal serial speed on assimilation: false
3 Device configuration pull method: console
4 Device configuration push method: xmodem
5 Alternative device configuration push method: tftp
6 Device configuration push retries: 3
7 Automatic configuration rollback: [disabled/manual/automatic] manual
8 Count delay before automatic configuration rollback: 75
9 Issue 'write memory' after configuration rollback: true
10 Verify OS upgrade: true
11 Use manual boot during upgrade, if applicable: true
12 OS image push method: tftp
13 Alternative OS image push method: xmodem
14 Attempt to use XModem-1K (first attempt only): true
15 Save Configuration on change before reboot? true
16 Include current running-config in exports? false
17 Previous OS image not found, continue? true
18 Maximum OS image push retry attempts: 3
19 Device reboot timeout (seconds): 300
20 Force the device to reboot immediately after pushing the OS: true
21 Device pass through timeout(seconds): 300
22 Enable local echo: false
23 Leave old OS if space permits during OS upgrade: true
24 Pull config before 'terminal' if local copy is older than (minutes)? 180

```

# In the Uplogix web interface

**Inventory > group page > System > Default Port Settings** - inherited from this group

**Inventory > Local Manager page > System > Default Port Settings** - inherited from this system

**Inventory > system page > port detail> Port Settings** - specific to this device

# History 
3.1 This command was introduced to replace show preferences.

# Related commands 

- **config settings**
