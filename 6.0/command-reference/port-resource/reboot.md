<!-- 5.4 -->

Reboots the device connected to this port. Rules can be defined to automate this operation using the reboot action.

Use the restart command to reboot the Uplogix Local Manager.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All

LMS offerings: All

#Syntax 

```
reboot
```

# Usage 

A reboot is considered successful when all of the expected checkpoints in the reload have passed.

```
[admin@UplogixLM (port1/1)]# reboot
Issuing 'reload'
Reading post
Bootstrap posted
C2600 platform with 65536 Kbytes of main memory
Image decompressing
Image decompressed
Device loaded
Post complete.
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > Local Manager page > port detail > schedule** - specific to this device

# History 
--

#Related commands 

**power**
**restart** 
