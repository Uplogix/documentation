# Overview

The purpose of this document is to detail the installation and configuration of iDirect satellite modems for use with Uplogix appliances. 

# Supported Models

LMS 6.0 includes support for iDirect satellite modems including 8000, 7000, 5000, 3000, X3, X5 series standalone, and iConnex models.

# Driver Features
* Option File Management â€“ Ability to store and manage multiple versions of option files on the Uplogix appliance 
	* Configuration change detection and automated rollback
	* Capture extended configuration elements outside the option file
	* Restore from corrupt option file
* Operating System Management â€“ Store and install specific package or operating system images
* Key Parameter Monitoring â€“ Maintaining a database of historical operational statistics	
	* RF Parameter Monitoring - monitor operational Radio Frequency (RF) elements
	* Interface Monitoring - ability to monitor Ethernet and tunnel interfaces
	* Console Message Logging - monitor console log messages
* Capturing Raw Buffer Logs â€“ Current and previous raw interaction logs are available for review
* Automating Actions â€“ Executing common maintenance tasks on demand or as a series of automated actions 
	* Set latitude/longitude position â€“ Because the Uplogix uses transmit and receive pins of the iDirect console port to interact, the NMEA-183 output of a GPS antenna cannot be plugged directly into the console port and must be monitored on another Uplogix port.
	* Interface on/off/cycle
	* Reboot
	* Power on/off/cycle
	* Executing single line commands and parsing the results

# Physical Installation

## Terrestrial Environment

In a terrestrial or fixed installation, connect a standard Cat5/patch cable between an available Uplogix port and the console port of the iDirect modem.

## Maritime/Mobile Environment

In the maritime or mobile environments, key information is passed between the antenna and the modem. With the Uplogix appliance managing the modem via a console connection, it is necessary to create a split cable for this information to pass directly between the antenna and modem uninterrupted. There are two pins carrying key information between the antenna and the modem: RJ-45 pin 2 which carries the AGC threshold information and RJ-45 pin 7 which carries TX Mute. Below is an example wiring diagram describing the split cable configuration. This cable is available as Uplogix part number UP610031 CABLE,UPLOGIX-iDIRECT-SEATEL NO CONNECTOR, or UP610033 CABLE,UPLOGIX-iDIRECT-SEATEL DB25.
 
![RJ-45 Plug](http://uplogix.com/support/docs/img/configuration-guides/idirect-image001.png)

For example, the Sea Tel terminal mounting strip wiring diagram is displayed below.

![Sea Tel Mounting Strip](http://uplogix.com/support/docs/img/configuration-guides/idirect-image002.jpg)
 
# Configuring the Port

Use a workstation to open a command line session with the Uplogix appliance.

Issue the **port** command to switch to navigate to the port your iDirect modem is connected to. In the example below the iDirect modem is attached to port 2.

```
[admin@UplogixLM]# port 1/2
native
[admin@UplogixLM (port 1/2)]#
```

Use the **config init** command to configure the port for iDirect.

```
[admin@UplogixLM (port1/2)]# config init
--- Enter New Values ---
description: []: iDirect
make: [embedded]: iDirect
model: 
os: []:infiniti
os version: []:
management IP: []:
configure dedicated ethernet port? (y/n) [n]:
console username: []: root
console password []: ********
confirm console password []: ********
enable username: []: admin
enable password []:********
confirm enable password []:********
serial bit rate [9600]: 9600
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
use null modem (rolled cable to device)? (y/n): n
Do you want to commit these changes? (y/n): y
```

Issue the **terminal** command to start a terminal session with the modem. This session takes place within your Uplogix appliance session.

```
[admin@UplogixLM (port1/2)]# terminal
Press ~[ENTER] to exit
Connecting ...

Retrieving running-config from device ...
Complete. config pulled.
running-config saved to archive as current.

Console session started.
```

Upon login you should see the iDirect prompt.

```
[RMT:361] admin@telnet:127.0.0.1
>
```

# Automated Functions

## Configuring Monitors

Monitors collect chassis and interface data from supported devices. The results can be used to trigger an alarm, event or to take other automated actions. There are six monitors for the iDirect modem: chassis, interface, remotestate, ping, consoleLog and terminal. 

* Chassis â€“ Checks the status of the iDirect with regards to CPU usage, Falconâ€™s status, configuration errors, temperature and memory. 
* Interface â€“ Captures information on the Ethernet and tunnel interfaces and includes RX/TX bytes, interface resets, link state, etc.
* Remotestate â€“ Checks the status of the iDirect with regard to receive and transmit power, frequency and errors, FSD, IGroup, HDLC, CompID, receive lock, link layer, modem state, receive AGC, receive signal-to-noise ratio and receive tmdlost. 
* Ping â€“ Executes an ICMP ping to a specified IPv4 address from the modemâ€™s context. The results can be displayed with the show pingstats command.
* ConsoleLog â€“ Captures system error logs as they are displayed via the console. The results may be displayed with the show device syslog command.
* Terminal â€“ Captures user interactions with the device. 

When the modem is initialized using the **config init** command, the chassis and console log monitor will automatically be scheduled. 

Additional monitors to capture information on RF statistics from the modem can be scheduled using the config monitor <monitor> command at the port level. For example, the remotestate monitor is scheduled using the command:

```
[admin@UplogixLM (port1/2)]# config monitor remotestate
``` 

The results of monitors can be viewed with the show <monitor> command with two options: -n <count> to display multiple chronological values, and -t which will add an elapsed time value to the results.

## Example #1

![](http://uplogix.com/support/docs/img/configuration-guides/idirect-image003.png) 

## Example #2

![](http://uplogix.com/support/docs/img/configuration-guides/idirect-image004.png) 

## LatLong (GPS Coordinates)

In maritime/mobile configurations, the Uplogix may be required to regularly supply GPS coordinates to the iDirect over the console port. In order to provide this information accurately, the Uplogix must have a source for GPS coordinates with data no more than two hours old. The Uplogix can monitor an external GPS source such as a shipâ€™s compass or dedicated GPS antenna to capture this information. 

Additionally, the coordinates may be monitored from a supported antenna controller. 
Once the coordinates are collected by the Uplogix appliance, they can then be sent to the iDirect on a configurable basis using the **config schedule** command at the port level. In the example below, the scheduled task sends the coordinates to the iDirect every 60 seconds by issuing the iDirect latlong command on the console.

```
config schedule setPosition -d 60
``` 

GPS coordinates may also be issued as a response to the Consolelog monitor.

## Event Logging (Syslog)

Collecting and monitoring syslog messages from the iDirect modem is configured with the config init command and can be viewed by issuing the following command:

```
show device syslog
```

A rule can then optionally be applied to check for string matches allowing for log analysis and action-based responses. In the example below, the appliance is configured to search for a message indicating the GPS coordinates are not available and send the coordinates when that event occurs.

```
config monitor consoleLog Send_Lat_Lon_On_Unavailable_Message
``` 

# Advanced Features

## Uplogix File System

The Uplogix file system is a repository for configuration, OS and post files for the managed iDirect.

To view the files in the Uplogix file system for your device, use the **show directory** command:

```
[admin@UplogixLM (port1/1)]# show directory
Type   Version  Name
------- --------- ------------
Config
  Running
     Current  running-config
     Previous  running-config

  Startup
     Current  startup-config
     Previous  startup-config

OS
     711    remote-7_1_1.pkg

Post
     Current  readPost
```

## Named Files

Users can name specific versions of configurations and operating system files. These named versions can be referenced in rules. For more information about our user named versions please see the User-Defined Versions Feature Guide.

## Option File Management

Uplogix RMOS supports management of option files. The startup configuration and running configuration can be pulled from the iDirect and saved on the Uplogix using the pull command. In addition, the running configuration, startup configuration, and operating system images saved on the Uplogix can be pushed to the iDirect using the push command. Finally, all of the files stored on the Uplogix can be copied to or from the port using the copy command. 

![](http://uplogix.com/support/docs/img/configuration-guides/idirect-image005.png) 

The Local Manager can be used to manage the running configuration which contains the startup configuration (falcon.opt or show Option file) and also various runtime parameters. Managing a running configuration through Uplogix will use options set commands for each parameter and can rollback changes accordingly if required. 

When pushing a new running configuration, reboot is available with the â€“reboot switch. The command for pushing the running configuration is **push running-config <previous|candidate|current|<user ver>> [-reboot]**

The Local Manager can also be used to manage the startup configuration which contains the option file (falcon.opt). When managing startup configurations through Uplogix, the appliance will utilize the Linux interface and push over the falcon.opt file rather than set the individual parameters in the Falcon interface. Pushing the startup configuration also allows an optional service level or system level reboot upon confirmation.

## Operating System File Management

Uplogix supports management of operating system files. Both Base Software Packages (BSPs) and Remote Application files can be copied from and pushed to the iDirect via the Uplogix. 

To copy operating system candidates to the iDirect port, use the **copy** command.

The Uplogix iDirect driver has the ability to push operating system images to the iDirect with the **push os** command. Pushing an operating system requires IP connectivity from the Uplogix to the iDirect. In the example below, the operating system file, 1003 is pushed to the iDirect.

```
[admin@UplogixLM (port1/2)]# push OS 1003
Transfering 3893765 bytes
Verifying checksum: 8b8897b7ac1fd854e46f29cf146ff416
Wating for package install (up to 300 seconds)
Issuing 'request system reboot'
Reading post
Device loaded
Post complete.
Hostname   :
Serial Number: 288
Make     : iDirect
Model    : X5
OS Type   : iNFINITI
OS Version  : app:10.0.0.3, bsp:10.0.0.3
Uptime    : 0 mins 8.32 secs
Push OS succeeded.
```

When pushing BSPs and Remote Application (the Falcon Service) files, it is required to push the BSP first, as it should be kept at a higher version # than the Remote Application.

The Uplogix iDirect driver does not have the ability to retrieve the Package Files from a managed iDirect device, but they remain in the Uplogix file system as an operating system candidate when the Uplogix performs the upgrade process.