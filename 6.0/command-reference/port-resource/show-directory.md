<!-- 5.4 -->

Displays files stored for each supported device.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show directory [-v]
```

The **â€“v** parameter ads file size and date display.

# Usage 

Files are associated with a particular port, make, model, and OS combination. If you change a device on one of the Uplogix Local Managerâ€™s ports, the files will not be accessible from that device unless it is a similar make, model, and OS combination.

```
[admin@UplogixLM (port1/3)]# show directory
Type    Version   Name
------- --------- ------------
Config
  Running*
        Current   running-config
        Previous  running-config

  Running-Undo*
        Candidate running-config-undo43414.img

OS
        DAC606    DAC-2202_ 606.s19
```

# History 

1.4 - The verbose flag (-v) was modified to display archived versions of device files.

# Related commands 

- **copy**
