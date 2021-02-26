<!-- 5.4 -->

Displays collected interface statistics and any current alarms on the specified interface.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Juniper, Netscreen, Nortel, Tasman, TippingPoint

Uplogix Local Managers: All

LMS offerings: All

# Syntax 
```
show interface <â€œinterface nameâ€> [-n <#>]
```

**-n <#>** â€“ number of records to display

# Usage 

Statistical data is purged from the local database based on available disk space but is available via export or archive for long term access.

Service module data is displayed using the **show service-module** command.

```
[admin@UplogixLM (port 1/1)]# show interface FastEthernet0/0
Displaying Interface Config
---------  --------- -----
Found 1  config entries for interface in the database.
Admin Status: up                        Arp Timeout: 04:00:00
Arp Type: ARPA                          Autonegotiation: N/A
Bandwidth: 100000                       Delay: 100
Encapsulation: ARPA                     Local Manager Device: N/A
Full Duplex Mode: N/A                   Hardware: AmdFE
Id: 79a07db2-001e-11d9-a528-00a0f000fa01
Input Flow Control: N/A                 Ip Address: 66.193.254.226/29
Keep Alive Set: N/A                     Loopback Set: false
Mac Address: 0005.5ed0.cd40             Media Type: N/A
Mtu: 1500                               Output Flow Control: N/A
Queueing Strategy: fifo                 Timestamp: 2004-09-06 16:04:47.372
-----
Displaying Interface Statistics
---------- --------- ----------
Found 1  statistical entry for interface in the database.
Local Manager Device: N/A
Id: 9a2a69be-001e-11d9-a528-00a0f000fa01
Input Aborted Packets: 0                Input Alignment Errors: 0
Input Broadcast Packets: 4220           Input Bytes: 3873849709
Input CRC Errors: 0                     Input Dribbles: 0
Input Errors: 0                         Input Frame Errors: 0
Input Frames: 0                         Input Giants: 0
Input Ignored Packets: 0                Input Lack Of Resource Errors: 0
< example text removed >
---------- ------ --- ---------
Found 0  alerts for interface in the database.
```
# History 
--

# Related commands 

- **config monitors**
- **show pingstats**
