<!-- 5.4 -->

Displays the result of the specified **pull tech** operation. This file provides details about the device that are helpful to technical support personnel in resolving any issues that may arise. Rules can be defined to include this operation using the showTech action.

# Command availability

CLI resource: port, modem

Device makes: Alcatel, Cisco, Netscreen

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show tech [current | previous | archive #]
```

# Usage 

This command only executes if the specified tech file exists. Otherwise, the CLI returns this message:

```
[admin@UplogixLM (port1/2)]# show tech
File does not exist. Run 'Pull Tech'
```

```
[admin@UplogixLM (port1/2)]# show tech
------------------ show version ------------------
Cisco Internetwork Operating System Software
IOS (tm) C2950 Software (C2950-C3H2S-M), Version 12.0(5)WC2b, RELEASE SOFTWARE (fc1)
Copyright (c) 1986-2002 by cisco System , Inc.
Compiled Fri 15-Feb-02 10:49 by devgoyal
Image text-base: 0x80010000, data-base: 0x8031E000
ROM: Bootstrap program is CALHOUN boot loader
AUS-DMZ uptime is 3 weeks, 4 days, 5 hours, 51 minutes
System returned to ROM by power-on
System image file is "flash:c2950-c3h2s-mz.120-5.WC2b.bin"
cisco WS-C2950-24 (RC32300) processor (revision B0) with 22249K bytes of memory.
Processor board ID FAB0551P1UH
Last reset from system-reset
---Press 'q' to quit, any other key to continue--- [1/50]
--output removed--
```

# In the Uplogix web interface

**Inventory > system page > port detail > Files > tech** - specific to this device

# History 
--
# Related commands 

- **pull tech**
