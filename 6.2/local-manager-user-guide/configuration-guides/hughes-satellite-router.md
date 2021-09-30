# Overview

The purpose of this document is to detail the installation and configuration of a Local Manager to manage and monitor a Hughes satellite router using a virtual serial port.

# Features

* Supports Hughes satellite routers with a Local Manager connected over the LAN.
* Monitors Hughes satellite routers for receiver lock and transmit errors.

# Configuring the Virtual Port

The Local Manager must have a route to the Telnet interface of the Hughes over the LAN.

To configure the virtual port for the Hughes, run the following commands on the system level of the Uplogix CLI, replacing 192.168.0.1 with the IP address of the Hughes, and 1953 with the TCP port of the Hughes' Telnet interface.

```
[admin@UplogixLM]# config system slot 4
[config system slot 4]# 1 192.168.0.1 1953 telnet
Port 1 added.
```

Navigate to the port and run **config init** to enter a description for the port.

```
[admin@UplogixLM (port4/1)]# config init
description []: Hughes HX200
make [native]:
management IP []: 192.168.0.1
Serial Bit Rate [9600]: 
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:
Do you want to commit these changes? (y/n): y
```

To test the connection, navigate to the newly configured port (4/1 in this example), type **terminal** to connect to the telnet interface, and enter the commands **c** and then **a** to query the Hughes for status.

```
[admin@UplogixLM]# port 4/1
native
Hughes HX200

[uplogix@Austin (port4/1)]# t 
Press ~[ENTER] to exit. 
Connecting ... 
Console session started. 
Press ~[ENTER] to exit. 
Satellite Interface Stats Menu:
(a) Display Main Statistics
(b) Display Traffic Statistics
(c) Display Satellite Interface Serial Number
(d) Display Signal Quality Factor
(e) Clear Statistics
(g) Display PEP Statistics
(i) Display Routing Statistics
(z) Return to Main Menu 

Satellite Interface Stats Menu (<?/CR> for options):
Satellite Interface Serial Number: 2551897 

Satellite Interface Stats Menu (<?/CR> for options):
------------------------------------
Local Time: THU JAN 29 14:45:06 2015
------------------------------------
Adapter Main Statistics:
------------------------
Signal Strength.............. 44 Stream Msg-Ackd/Nakd........ 9991061/874082
Flags............... 0x00000000 NonStream Msg-Ackd/Nakd..... 130323/41868
Stream Error Rate....... 8.04% NonStream Error Rate....... 24.31%
UpTime (d:h:m:s).. 026:11:39:58 Aloha Starts................ 130419
WakeUp Aloha Starts.......... 628 Ranging Starts.............. 0
Transport Alarm Bit..... 0x0000 Frames Received............. 53588119
Addresses Open............... 8 Frame Errors: CRC/Bad Key... 0/0
Carrier Info....... 097:W:09671 Miscellaneous Problems...... 11555
Rate Code........ 256k 4/5 (TC) No Receive Outroute Lock.... 696323
Inroute Group................ 2 No FLL Lock................. 185419
Inroute..................... -1 No Network Timing Sync...... 10448
IQoS ID...................... 21 Spreading Factor ........... 2
10 MHz Ref Clock............. Internal
Current Modcod............... QPSK 3/4 (7) 

Ranging Reason: Ranging Done
Inroute Group Selection: Ranged at inroute rate selected by IQoS 

Receive Status: Receiver operational. (RxCode 5)
Transmit Status: Transmitter ready. (TxCode 8) 

Satellite Interface Stats Menu (<?/CR> for options):
```

# Rules

The Local Manager can automatically monitor the Hughes for receiver lock and transmit errors. To configure the Local Manager with the required rules, copy and paste the following rules into the CLI of the Local Manager.

```
config rule no hughesCheck
config rule hughesCheck
conditions
true
exit
action execute -command "\" -pattern "."
action execute -command "c" -pattern "."
action execute -command "a" -setValue monitor hughesRxCode $1 -pattern "RxCode (\d+)" -multiline 
action execute -command "c" -pattern "."
action execute -command "a" -setValue monitor hughesTxCode $1 -pattern "TxCode (\d+)" -multiline 
exit

config rule no hughesRx
config rule hughesRx
conditions 
NOT compare-value monitor hughesRxCode = 5 
exit 
action alarm GENERIC -a "receiver not locked"
exit

config rule no hughesTx 
config rule hughesTx 
conditions 
NOT compare-value monitor hughesTxCode = 8
exit 
action alarm GENERIC -a "transmit error"
exit

config ruleset no hughes
config ruleset hughes
rules
hughesCheck | hughesRx | hughesTx
exit
exit
```

# Monitor

To configure the Local Manager to check the Hughes for errors, navigate to the serial port the Hughes is connected to and run the following command.

```
[admin@UplogixLM (port4/1)]# config monitor chassis hughes
Validate scheduled monitor(chassis)? (This will execute the job now.) (y/n): y
Job was scheduled 29: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor chassis 30
```