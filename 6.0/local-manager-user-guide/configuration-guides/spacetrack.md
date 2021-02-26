# Overview

The purpose of this document is to detail the installation and configuration of a SpaceTrack4000 Antenna Controller Unit (ACU) for use with Uplogix appliances.  

# Terminology

Acronyms and abbreviations used in this document:

* ACU â€“ Antenna Controller Unit
* M&C â€“ Managing and Controlling 
* BDU â€“ Below Deck Unit

# Configuring the Port

A few important items to note prior to configuration: 

* The default baud rate for the Spacetrack M&C port is 9600.
* The default password for the BDU is FACTORY SETUP.

Once the Spacetrack BDU is properly connected to the Uplogix appliance, take the following steps to configure the port:

Open a connection to the Uplogix Local Manager and navigate to the port you wish to initialize.

```
[admin@UplogixLM]# port 1/1	
 native
[admin@UplogixLM (port 1/1)]# 
```

Use the **config init** command to configure the M&C port on the Spacetrack 4000. The make and OS should both be set to Spacetrack. Model and OS version are not required.  

```
[admin@UplogixLM (port 1/1)]# config init
--- Enter New Values ---
description: []: 
make: [native]: Spacetrack
model: []: 
os: []: Spacetrack
os version: []:
management IP: []:  
Configure dedicated Ethernet port? (y/n) [n]: 
console username: []:  
console password []: FACTORY SETUP
confirm password: FACTORY SETUP
enable username: []:FACTORY SETUP
enable password []:FACTORY SETUP
serial bit rate [9600]: 9600
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
Do you want to commit these changes? (y/n): y
```

When the **config init** command completes, run **terminal** to open a terminal session with the Spacetrack ACU. The Uplogix appliance will locally echo the commands to make interactions easier.

```
[admin@UplogixLM (port 1/1)]# terminal
Press ~[ENTER] to exit 
Connecting ... 
beginning pull of running-config
running-config saved to archive as current.
Console session started.
```

If the port has been properly configured, you will be able to interact with the ACU using standard command codes. If you are not able to interact with the 4000 ACU using the appropriate command codes, ensure that the physical connection is correct and that the serial settings on the Uplogix appliance match those on the 4000 ACU.  Use the escape sequence (~[ENTER]) to exit the terminal session with the ACU.

# Automated Functions

Automated jobs are scheduled using default frequency during the config init process. For the Spacetrack ACU, these jobs include pullRunningConfig and deviceInfo.

## Running Config
The 4000 ACU has one configuration file that is pulled by the pullRunningConfig job and is stored on the appliance as the running-config. To pull this file manually, use the **pull running-config** command.

```
[admin@UplogixLM (port1/1)]# pull running-config
beginning pull of running-config
running-config saved to archive as current.
```

## Configuration Rollback

The Spacetrack ACU driver includes support for Surgical Rollback. When the **terminal** command is run, the appliance will pull the device configuration before giving control to the user. After the terminal session is closed, the device configuration will be pulled again and compared to the original. If the session was terminated unexpectedly, any changes will be rolled back. Otherwise, the user will be presented with the options to commit or rollback any changes made.

## Configuring Monitors

There are two monitors that are automatically scheduled when a port is configured as a Spacetrack ACU: 

* **gps:** Collects latitude and longitude information from the ACU.  
* **remotestate:** Collects information on key variables including azimuth, relative azimuth, cross level, AGC, AGC threshold, and polarity angle.

The monitors are scheduled to run at 30 second intervals by default. If you would like to change the monitor interval, simply reschedule the monitor with the appropriate delay. The syntax for scheduling a monitor is:

```
config monitors <object> <interface> [ruleList] [:delay]
```

To schedule the monitors for the Spacetrack ACU, navigate to the port of the device to be monitored.

```
[admin@UplogixLM]# port 1/1
SpaceTrack 4000 
SpaceTrack4000
```

Use the **config monitors** command to schedule the specific monitor.

```
[admin@UplogixLM (port1/1)]# config monitors gps :60
Job was scheduled 1: [Interval: 60 Seconds; Mask: * * * * *] rulesMonitor gps
```

GPS information is now being monitored.

```
[admin@UplogixLM (port1/1)]# config monitors remotestate :30
Job was scheduled 2: [Interval: 30 Seconds; Mask: * * * * *] rulesMonitor remotestate
remotestate information is now being monitored.
```

## Displaying Monitors

To display monitor data, use the **show** command from the port. The command syntax is:

```
[admin@UplogixLM (port 1/1)]# show monitors
```

The result will display index number, time interval and mask, interface name, applied rules, and delay time.

```
1: [Interval: 00:00:60 Mask: * * * * *] rulesMonitor gps none â€œâ€ 60
2: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor remotestate none â€œâ€ 30
```

## Displaying GPS Data

The GPS monitor is displayed in three parts: events, most-recent, and position. These extensions are required for display of the GPS data. The extensions are described below: 

* Events: Shows GPS coordinates associated with Uplogix events
* Most-recent: Displays the most recent valid GPS coordinate
* Position: Displays the GPS coordinate history

Examples of the three GPS monitors:

```
[admin@UplogixLM (port1/1)]# show gps events
GMT      Latitude             Longitude        Context  Message
---      -----------------    ---------------  -------  -------------------------------
11/26    57d 7' 12.000" N     2d 6' 36.000" W           Pull running config completed.
11/26    57d 7' 12.000" N     2d 6' 36.000" W           User started a terminal session.
11/26    57d 7' 12.000" N     2d 6' 36.000" W           User completed a terminal session. 
11/26    57d 7' 12.000" N     2d 6' 36.000" W           User started a terminal session.
11/26    57d 7' 12.000" N     2d 6' 36.000" W           User completed a terminal session. 
11/26    57d 12' 36.000" N    2d 6' 36.000" W           Pull running config completed.
11/26    57d 12' 36.000" N    2d 6' 36.000" W           Pull running config completed.
11/27    57d 12' 36.000" N    2d 6' 36.000" W           Pull running config completed.
11/27    57d 12' 36.000" N    2d 6' 36.000" W           Pull running config completed.
11/27    57d 12' 36.000" N    2d 6' 36.000" W           Pull running config completed.

[admin@UplogixLM (port1/1)]# show gps most-recent
Most-recent, port1/1:
GMT          Latitude              Longitude           Heading     Elevation     # Sats
--------     -----------------     ---------------     -------     ---------     ------
16:52:26     57d 12' 36.000" N     2d 6' 36.000" W         0.0           0.0          1
```

## Displaying Remotestate Data

To display monitor results, use the **show <monitor name>** command from the port.
 
```
[admin@UplogixLM (port1/1)]# show remotestate
```
 
## Displaying Device Syslog

To display syslog information for the SpaceTrack 4000, use the **show device syslog** command from the port.  This command will display currently stored syslog data.  The command syntax is:

```
[admin@UplogixLM (port1/1)]# sh device syslog
11/18/10 18:49:40.208    Remote Console logged out
11/18/10 18:49:40.232    Mode changed to Locking
11/18/10 18:49:40.247    Mode changed to Search
11/18/10 18:49:40.264    Mode changed to Locking
11/18/10 18:49:40.292    Mode changed to Track
11/18/10 18:49:40.307    System Initialised
11/18/10 18:49:40.323    Connected to a 80C167 ADU module
11/18/10 18:49:40.337    ADU auto balance capability detected
11/18/10 18:49:40.353    Mode changed to Find
11/18/10 18:49:40.368    Mode changed to Locking
11/18/10 18:49:40.383    Mode changed to Track
```