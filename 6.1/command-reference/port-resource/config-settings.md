<!-- 5.4 -->

Opens an editor to set the default options that the Uplogix Local Manager uses to interact with the device.

# Command availability 

CLI resource: port, modem

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Modem: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax

```
config settings
```

# Usage

```
[admin@UplogixLM (port1/1)]# config settings
--- Settings Menu ---
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
25 Done
Select setting to edit or 25 to end:


```
# In the Uplogix web interface

**Inventory > group page > System > Default Port Settings** - inherited from this inventory group

**Inventory > Local Manager page > System > Default Port Settings** - inherited from this system

**Inventory > Local Manager page > port detail > Port Settings** - specific to this device

# History

3.1 - This command was introduced to replace config preferences.

# Related commands

- **show settings**
