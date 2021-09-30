# Overview

The purpose of this document is to detail the installation and configuration of a Local Manager to manage and monitor a KNS antenna controller using a virtual serial port.

# Features

* Supports KNS antenna controllers with Local Managers connected over the LAN.
* Monitor KNS for tracking and lock errors.

# Configuring the Virtual Port

The Local Manager must have a route to the Telnet interface of the KNS over the LAN. 

To configure the virtual port for the KNS, run the following commands on the system level of the Local Manager CLI, replacing 203.0.113.16 with the IP address of the KNS, and 2502 with the TCP port of the KNS's Telnet interface (2502 is the default).

```
[admin@UplogixLM]# config system slot 4 
[config system slot 4]# 2 203.0.113.16 2502 telnet
Port 2 added.
```

Navigate to the port and run **config init** to enter a description for the port.

```
[uplogix@Austin (port4/2)]# config init
description []: KNS TTP
make [native]:
management IP []: 10.200.29.213
Serial Bit Rate [9600]: 
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:
Do you want to commit these changes? (y/n): y
```

To test the connection, navigate to the newly configured port (4/2 in this example), type **terminal** to connect to the Telnet interface, and enter the command **SM** to query the KNS for status.

```
[admi@UplogixLM]# port 4/2
native
KNS TTP

[admin@UplogixLM (port4/2)]# t

Press ~[ENTER] to exit.

Connecting ...

Console session started.  Press ~[ENTER] to exit.

SM: 111011111232020 00000100 N3022.5486 W09746.9757 01 -097.0 1619 3426 1089 0000 0213.2 058.5 0000.0 0202.8 0064.0
```

# Monitoring the KNS

## Rules

The Local Manager can automatically monitor the KNS for errors with DVB lock and tracking. To configure the Local Manager with the required rules, copy and paste the following rules into the CLI of the Local Manager.

```
config rule no knsCheck
config rule knsCheck
conditions
true
exit
action execute -raw -command "SM\r" -setValue monitor knsDvbAgc $4 -setValue monitor knsSatId $3 -setValue monitor knsDvbCode $2 -setValue monitor knsTrackingCode $1 -pattern ":\s\d(\d)(\d)\d\d\d\d\d\d\d\d\d\d\d\d\s\d\d\d\d\d\d\d\d\s[NS].+\s[WE].+\s(\d\d).+\s.+\s(\d\d\d\d)"
exit

config rule no knsTracking
config rule knsTracking
conditions
compare-value monitor knsTrackingCode = 0
exit
action alarm GENERIC -a "KNS not tracking"
exit

config rule no knsDvb 
config rule knsDvb 
conditions
compare-value monitor knsDvbCode = 0
exit
action alarm GENERIC -a "KNS DVB not locked"
exit

config ruleset no kns
config ruleset kns
rules
knsCheck | knsTracking | knsDvb
exit
exit
```

## Monitor

To configure the Local Manager to check the KNS for errors, navigate to the serial port the KNS is connected to and run the following command.

```
[admin@UplogixLM (port4/2)]# config monitor chassis kns
Validate scheduled monitor(chassis)?  (This will execute the job now.) (y/n): y
Job was scheduled 29: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor chassis 30
```