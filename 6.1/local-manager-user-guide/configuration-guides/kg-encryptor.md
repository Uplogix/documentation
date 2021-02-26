# Overview

The purpose of this document is to detail the installation and configuration of an Uplogix Local Managers (LM) to facilitate remote connectivity to a KG Encryptor.

# Features
* Supports KG-175A Encryptors with Uplogix Local Manager
* Supports KG-175D Encryptors with Uplogix Local Manager with dedicated Ethernet card installed

# Physical Connection

## KG-175A 

Connect a free serial port on the Uplogix to the KG-175Aâ€™s RS-232 console management port with a standard Cat-5 cable and a RJ45-to-DB9 connector. 

## KG-175D
Connect the Uplogix LMâ€™s corresponding Ethernet port to the KG-175Dâ€™s front-panel-mounted
 Ethernet Port provided for the Console with a standard Cat-5 cable.

> A dedicated Ethernet connection is required for Ethernet port forwarding.  This type of connection is supported on an Uplogix LM with an installed dedicated Ethernet card.

# Configuring the Ports

## KG-175A 

To configure the LM for connection to a KG-175A, run the command **config init** and follow the prompts as below:

```
[admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: KG-175A
make [native]: 
management IP: 
Configure dedicated ethernet port? (y/n) [n]: n
Serial Bit Rate [9600]: 
Serial Data Bit [8]: 
Serial Parity [none]: 
Serial Stop Bit [1]: 
Serial Flow Control [none]: 
Use null modem (rolled cable to device)? (y/n) [n]: 
Do you want to commit these changes? (y/n): y
```
The default console settings for the KG-175A are 9600 bit rate, 8 serial data bit, no serial parity, serial stop bit 1, no flow control.

## KG-175D 

To configure the Uplogix LM for connection to a KG-175A, run the command **config init** and **config protocol forward** and follow the prompts as below:

```
[admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: KG-175D
make [native]: 
management IP: 
Configure dedicated ethernet port? (y/n) [n]: y
Use DHCP? (y/n) [n]: n
Each dedicated port IP address assignment must be on a different network.
The device IP assignment and port IP assignment should be on the same network for this port.
dedicated device IP: 172.16.0.1
dedicated port IP: 172.16.0.2
dedicated netmask: 255.255.255.0
speed/duplex [auto]: 
Serial Bit Rate [9600]: 
Serial Data Bit [8]: 
Serial Parity [none]: 
Serial Stop Bit [1]: 
Serial Flow Control [none]: 
Use null modem (rolled cable to device)? (y/n) [n]: 
Do you want to commit these changes? (y/n): y
```

To configure the Local Manager to pass web traffic to the KG-175Aâ€™s web interface, run the **config protocol forward** command as below and enter **dedicated 80 http** to set the TCP port to which traffic will be passed on the deviceâ€™s dedicated IP address (172.16.0.1, entered above).

```
[admin@UplogixLM (port1/4)]# config protocol forward
[forward]# dedicated 80 http
[forward]# exit
```

# Connecting to the Encryptor

## KG-175A 

To connect to the serial console of the KG-175A, first connect to the Uplogix LM using SSH, navigate to the port that the KG-175A is connected to, and use the **terminal** command. When finished, use **~ <ENTER>** to disconnect.

```
[admin@UplogixLM]# port 1/4
native
        KG-175A

[admin@UplogixLM (port1/4)]# terminal
Press ~[ENTER] to exit.
Connecting ...
Console session started.  Press ~[ENTER] to exit.
Console session ended.
Disconnecting ...
```

## KG-175D

The methodology for connecting to the web interface of a KG-175D varies slightly depending on the SSH client being used.
 
To use the SSH applet in the Uplogix Control Centerâ€™s GUI, click the CLI button for the Uplogix LM, log in with valid credentials, click Terminal > Forward, click the check box next to the KG-175Dâ€™s port, then click Apply. 

![](http://uplogix.com/support/docs/img/configuration-guides/kg-image001.png)
 
A connection to the KG-175Dâ€™s web interface can now be achieved by opening a web browser on your workstation and entering **127.0.0.1:[port]** in the address bar, where [port] is the port highlighted in green (6252 in the above example). The port is selected randomly when Apply is pressed, but can also be set manually by entering a port number and pressing Apply.