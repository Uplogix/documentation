<!-- 5.4 -->

This command power cycles the device and breaks its normal boot sequence. Then it replaces its configuration with the last stored current one. 

This command requires power control and is only available for Cisco routers running IOS or CatOS, and Cisco switches running CatOS.

# Command availability

CLI resource: port

Device makes: Cisco

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
recover configuration
```

#Usage 

```
[admin@UplogixLM (port1/1)]# recover configuration
Attempting to revert startup configuration to current from 14 Aug 21:57
Powering off outlet(s) [1, 2]
DSR was active.
CTS was active.
CTS is still active.
Powering on outlet(s) [1, 2]
Serial link is active.
Attempting to break into ROMmon mode.
Break into ROMmon successful.
Reading post
Image decompressing
Image decompressed
Post complete.
```

# History 

1.1 â€“ This command was introduced; it replaces recover password.

# Related commands 

- **push running-config**
