# Overview

The purpose of this document is to detail the installation and configuration of a Tracstar AVL Antenna Controller Unit (ACU) and an iDirect Satellite Modem for use with Uplogix Local Managers.

# Features

* Supports Tracstar ACUs in DirectPoint (LOCK mode 10000) or in Satellite Reference mode (LOCK mode 1022) 

# Physical Connection

Connect the Tracstar and iDirect serially to available ports on the Uplogix Local Manager. The iDirect's console connection is used to interactively manage the iDirect, monitor the state of the modem, and provide it with GPS data. The Tracstar's modem connection is used to collect GPS information from the ACU. Both connections will be used to pass RX SNR data between the Tracstar and iDirect.

Connect the Uplogix to the Tracstar's modem port (MOD) with a DB9 to RJ45 straight cable.

![](http://uplogix.com/support/docs/img/configuration-guides/tracstar-image001.png)
  
Connect the Uplogix to the iDirect's console port with a RJ45 to RJ45 straight cable.

![](http://uplogix.com/support/docs/img/configuration-guides/tracstar-image002.png) 

# Configuring the Ports

## Tracstar Port Initialization

Once the Tracstar ACU and iDirect are properly connected to the Uplogix Local Manager, take the following steps to configure the ports.

Open a connection to the Uplogix Local Manager and navigate to the port that the Tracstar is connected to.

```
[admin@UplogixLM]# port 1/3	
 native
```

Use the **config init** command to configure the port for use with the modem port on the Tracstar ACU. The make should be Tracstar and the OS infiniti. Model and OS version are optional fields and will not be used. Press [Enter] when accepting default values.  Set the serial bit rate at 4800.

```
[admin@UplogixLM (port 1/3)]# config init
--- Enter New Values ---
description: []: Port Fore Antenna
make: [native]: Tracstar
model: []: 
os: []: infiniti
os version: []:
management IP: []: 
Configure dedicated Ethernet port? (y/n) [n]: 
console username: []: 
console password []: 
confirm password: 
enable username: []:
enable password []:
serial bit rate [9600]: 4800
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
Do you want to commit these changes? (y/n): y
```

When the **config init** command completes, run **terminal** to open a terminal session with the Tracstar. 

```
[admin@UplogixLM (port 1/3)]# terminal
Press ~[ENTER] to exit 
Connecting ... 
beginning pull of running-config
running-config saved to archive as current.
Console session started.
```

If the port has been properly configured, you will be able to see the Tracstar requesting RX SNR information. If you are not able to see the Tracstar's requests, ensure that the physical connection is correct and that the serial settings on the Uplogix Local Manager match those on the Tracstar ACU. Use the escape sequence (~[Enter]) to exit the terminal session with the ACU.

## Scheduling Tracstar Monitors

Schedule the GPS monitor to collect location data from the Tracstar with the command **config monitor gps :10**.

When asked to validate the monitor, select *n*.

```
[admin@UplogixLM (port1/1)]# config monitor gps :10
Validate scheduled monitor(gps)?  (This will execute the job now.) (y/n): n
Job was scheduled 19: [Interval: 00:00:10 Mask: * * * * *] rulesMonitor gps none 10
```

## Set Tracstar Properties

Next, set a properties field that will be used by the Uplogix LMS software to facilitate communication between the Tracstar and the iDirect. Enter **config properties**, then _idirect_port port x/y where port x/y is the port that the iDirect is connected to, then exit.

```
[admin@UplogixLM (port 1/3)]# config properties
[config properties]# _idirect_port port1/4
[config properties]# exit
```

# iDirect Port Initialization

Navigate to the port that the iDirect is connected to. 

```
[admin@UplogixLM]# port 1/4	
 native
```
 
Use the **config init** command to configure the port for use with the console port on the iDirect. The make should be iDirect and the OS infiniti. Model and OS version are optional fields and will be automatically populated during the inilitazation process. Press [Enter] when accepting default values.

``` 
[admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: []: iDirect satellite modem
make: [native]: iDirect
model: []:
os: []: infiniti
os version: []:
management IP: []:
console username: []: root
console password []: *******
confirm console password []: *******
enable username: []: admin
enable password []: *******
confirm enable password []: *******
serial bit rate [9600]: 4800
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
Do you want to commit these changes? (y/n): y
```

When the **config init** command completes, run terminal to open a terminal session with the iDirect. 

```
[admin@UplogixLM (port 1/4)]# terminal
Press ~[ENTER] to exit 
Connecting ... 
beginning pull of running-config
running-config saved to archive as current.
Console session started.
```

If the port has been properly configured, you will be able to see the iDirect's command prompt and interact with the modem's command line interface. If you are not able to interact with the iDirect, ensure that the physical connection is correct and that the serial settings on the Uplogix Local Manager match those on the iDirect. Use the escape sequence (~[Enter]) to exit the terminal session with the iDirect.

## Scheduling iDirect Monitors

To feed GPS data to the iDirect, schedule the set position job to run every 30 seconds.

```
[admin@UplogixLM (port1/4)]# config schedule setPosition -d 30
Validate scheduled job(setPosition)?  (This will execute the job now.) (y/n): n
Job 18 was scheduled.
```

Configure the remote state monitor by entering **config monitor remotestate :10**

```
[adnin@UplogixLM (port1/2)]# config monitor remotestate
Validate scheduled monitor(remotestate)?  (This will execute the job now.) (y/n): n
Job was scheduled 9: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor remotestate none 10
```

## Set iDirect Properties

Finally, set a properties field that will be used by the Uplgoix LMS software to facilitate communication between the Tracstar and the iDirect. 

```
[admin@UplogixLM (port 1/4)]# config properties
[config properties]# _tracstar_port port1/3
[config properties]# exit
```