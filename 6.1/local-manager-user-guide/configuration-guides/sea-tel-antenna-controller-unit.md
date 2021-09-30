# Overview
The purpose of this document is to detail the installation and configuration of a Sea Tel Antenna Controller Unit (ACU) for use with Uplogix Local Managers. 

# Features
* Supports DAC (ACU) software versions 4.10 and later

# Terminology

Acronyms and abbreviations used in this document:

* ACU - Antenna Controller Unit
* DAC - Digital Antenna Controller
* DacRemP - DAC Remote Panel
* M&C - Managing and Controlling 
* PCU - Pedestal Control Unit

# Physical Connection

There are two connection points from the Sea Tel ACU (M&C and NMEA) to the appliance. The M&C connection is used to interactively manage the Sea Tel ACU and PCU. The NMEA connection is used to collect GPS information in NMEA-183 format from the Sea Tel ACU. Both M&C and NMEA information may be retrieved from the M&C port. 

![ACU Physical Connections](http://uplogix.com/support/docs/img/lm-user-guide/seatel/seatel-panels.jpg)

The NMEA port should be used when the M&C will be utilized for extended interactive user sessions so GPS coordinates can be collected without interruption. 

The M&C port on the Sea Tel ACU can be connected to the Uplogix Local Manager with standard CAT5 cables and DB-9 to RJ-45 adaptors. The M&C port requires a rolled cable and the NMEA port requires a straight through cable.

# Configuring the Port

A few important items to note prior to configuration: 
* The default baud rate for the Sea Tel M&C port is 9600 on DAC 2202/2302/2200 series and 4800 on DAC 03/97 systems. The Uplogix appliance will need to be configured with the appropriate rate.
* The default baud rate for the Sea Tel NMEA port is 4800. If this value has changed, the Uplogix appliance will need to be configured with the new rate.
* The ACU's Serial M&C port does not require a username or password, although the initialization routine will ask for them. Bypass this prompt by hitting the return key.

Once the Sea Tel ACU is properly connected to the Local Manager, take the following steps to configure the port:

Open a connection to the Uplogix appliance and navigate to the port you wish to initialize.

Use the **config init** command to configure the port for use with the M&C port on the Sea Tel ACU. The make should be *SeaTel* and the OS *DAC*. Model and OS version are optional fields and will be populated automatically as part of the config init process. Press [Enter] when accepting default values.

```
[admin@UplogixLM (port 1/3)]# config init
--- Enter New Values ---
description: []: Starboard Aft Antenna
make: [native]: SeaTel
model: []: 
os: []: DAC
os version: []:
management IP: []: 
Configure dedicated Ethernet port? (y/n) [n]: 
console username: []: 
console password []: 
confirm password: 
enable username: []:
enable password []:
serial bit rate [9600]: 9600
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
Do you want to commit these changes? (y/n): y
```

When the **config init** command completes, run **terminal** to open a terminal session with the Sea Tel. 

```
[admin@UplogixLM (port 1/3)]# terminal
Press ~[ENTER] to exit 
Connecting ... 
beginning pull of running-config
running-config saved to archive as current.
Console session started.
```

If the port has been properly configured, you will be able to interact with the ACU using standard M&C commands (ie. "S" immediately returns the Status). If you are not able to interact with the Sea Tel ACU using the appropriate command codes, ensure that the physical connection is correct and that the serial settings on the Uplogix appliance match those on the Sea Tel ACU. Use the escape sequence (~[enter]) to exit the terminal session with the ACU.

The NMEA port should be used if NMEA formatted GPS is distributed to various services such as location coordinates to a modem or a location tracking program. Use the **config init** command to configure the port for use with the NMEA on the Sea Tel. The make should be *SeaTel* and the OS *NMEA*. Model and OS version are optional fields and will be populated automatically as part of the **config init** process.

```
[admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: []: Seatel GPS
make: [native]: seatel
model: []:
os: []: NMEA
os version: []:
management IP: []:
console username: []:
console password []:
enable username: []:
enable password []:
serial bit rate [9600]: 4800
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
use null modem (rolled cable to device)? (y/n) [y]: 
Do you want to commit these changes? (y/n): y
```

# Automated Functions

Automated jobs are scheduled using the assigned default intervals during the config init process. For the Sea Tel ACU, these jobs include pullRunningConfig and deviceInfo.

## Device Info

The deviceInfo job queries the Sea Tel ACU for information fields such as hostname, make, model, and OS version. By default, this job runs every 5 minutes. To view the collected data, use the show info command.

```
[admin@UplogixLM (port1/3)]# show info
Hostname: SS Envoy
Description: Starboard Aft Antenna
Make: SeaTel
Model: DAC 2202
OS: DAC
OS Version: 6.05
Management IP: 192.168.33.100
```

## Running Config

The Sea Tel ACU has one configuration file that is pulled by the pullRunningConfig job and is stored on the appliance as the running-config. To pull this file manually, use the **pull running-config** command.

```
[admin@UplogixLM (port1/3)]# pull running-config
beginning pull of running-config
running-config saved to archive as current.
```

## Configuration Rollback

The Sea Tel ACU driver includes support for Surgical Rollback, but is disabled by default. When the **terminal** command is run, the LM will pull the device configuration before giving control to the user. After the terminal session is closed, the device configuration will be pulled again and compared to the original. If any changes are detected, they will be reported in the device changes log and displayed to the user.  If Surgical Rollback is enabled, uncommitted changes will be rolled back.

## Configuring Monitors

There are two monitors that are automatically scheduled when a port is configured as Sea Tel: 

* gps: Collects latitude and longitude information from the PCU's integrated GPS (where available) from the M&C port. 
remotestate: Collects information on key antenna variables including heading, azimuth, relative azimuth, elevation, cross level, AGC, AGC threshold, and polarity angle. The monitors are scheduled to run at 30 second intervals by default. If you would like to change the monitor interval, simply reschedule the monitor with the appropriate delay. The syntax for scheduling a monitor is:
	
```
config monitors <object> <interface> [ruleList] [:delay]
```

To schedule the monitors for the Sea Tel ACU, navigate to the port of the device to be monitored.

```
[admin@UplogixLM]# port 1/3
SeaTel DAC 2202 DAC 6.05
```

Use the **config monitors** command to schedule the specific monitor.

```
[admin@UplogixLM (port1/3)]# config monitors gps :60
Job was scheduled 1: [Interval: 60 Seconds; Mask: * * * * *] rulesMonitor gps
```

GPS information is now being monitored.

```
[admin@UplogixLM (port1/3)]# config monitors remotestate :30
Job was scheduled 2: [Interval: 30 Seconds; Mask: * * * * *] rulesMonitor remotestate
```

Remotestate information is now being monitored.

## Displaying Monitors

To display scheduled monitors, use the **show monitors** command from the port. 

```
[admin@UplogixLM (port 1/3)]# show monitors
```

The result will display index number, time interval and mask, interface name, applied rules, and delay time.

```
1: [Interval: 00:00:60 Mask: * * * * *] rulesMonitor gps none "" 60
2: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor remotestate none "" 30
```

## Displaying Monitor Results

To display monitor data, use the **show** command from the port. The command syntax is:

```
show <monitor name>
```

For example:

```
[admin@UplogixLM (port1/3)]# show remotestate
Timestamp  Heading  Azimuth   Rel. Azimuth Elevation Cross Level   AGC        AGC polang
          (degrees) (degrees)    (degrees) (degrees)   (degrees)        Threshold
--------- --------- --------- ------------ --------- ----------- ------ --------- ------
15:27:48      317.6     343.4         25.7      89.4        90.0   1459      1520  212.0
15:27:26      317.6     343.1         25.4      89.4        89.9   1460      1520  212.0
15:26:48      317.6     342.6         25.0      89.4        89.9   1460      1520  212.0
15:26:26      317.6     342.3         24.7      89.5        90.0   1461      1520  212.0
15:25:48      317.6     341.8         24.2      89.4        90.0   1459      1520  212.0
15:25:10      317.6     341.3         23.7      89.4        90.0   1459      1520  212.0
15:24:48      317.6     341.0         23.3      89.4        90.0   1460      1520  212.0
15:24:11      317.6     340.5         22.8      89.5        89.9   1460      1520  212.0
15:23:48      317.6     340.2         22.6      89.5        89.9   1459      1520  212.0
15:23:11      317.6     339.7         22.0      89.4        90.0   1459      1520  212.0
15:22:40      317.6     339.2         21.7      89.4        90.0   1460      1520  212.0
15:22:10      317.6     338.8         21.4      89.4        90.0   1459      1520  212.0
```

GPS information is available in three areas: As an element to Uplogix alarms and events, as the result of the most-recent coordinate collection, and as a display only artifact in the GPS position. These extensions are required for display of the GPS data. The extensions are described below: 

* Events: Shows GPS coordinates associated with Uplogix events
* Most-recent: Displays the most recent valid GPS coordinate from multiple sources
* Position: Displays the GPS coordinate history

Examples of the three GPS monitors:

```
[admin@UplogixLM (port1/3)]# show gps events
CDT   Latitude          Longitude         Context Message
----- ----------------- ----------------- ------- -----------------------------------------
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         User started a terminal session.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation 90 succeeded
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation 0 succeeded
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation 45 succeeded
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation Range Test succeeded

[admin@UplogixLM (port1/3)]# show gps most-recent
Most-recent, port1/1:
CDT        Latitude            Longitude           Heading   Elevation   # Sats
--------   -----------------   -----------------   -------   ---------   ------
15:30:21   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1

[admin@UplogixLM (port1/3)]# show gps position
CDT        Latitude            Longitude           Heading   Elevation   # Sats
--------   -----------------   -----------------   -------   ---------   ------
14:59:46   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:00:24   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:00:46   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:01:23   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:02:01   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:02:24   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:17:51   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:18:13   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:18:50   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
```

For more information on the DAC commands utilized to collect the information in the driver monitors, please refer to appendix A of this document.

# Advanced Features

The Sea Tel driver offers several advanced features for interacting with the Sea Tel antenna system. This section describes upgrading a Sea Tel DAC or PCU, displaying additional system logging, and interacting with the DAC directly.

<div class='warning'>Not all versions of Sea Tel DAC and PCU code are compatible with all Sea Tel hardware. Ensure that the version of code you are upgrading to is compatible with the hardware. Upgrading the DAC or PCU to non-compatible code could place the Sea Tel in an unrecoverable state. CommIF module upgrades are only available on CommIF software versions 1.12 or later. Upgrading from a previous version will display an error.</div>

## Upgrading a Sea Tel DAC, PCU and CommIF

The Sea Tel advanced driver supports upgrades to the DAC, PCU, and CommIF module. CommIF upgrade requires CommIF software 1.12 or later to function. All components may be upgraded separately. Prior to upgrade, it is a best practice to stage the current working version of the ACU, PCU or CommIF code in the Uplogix' target port directory in the event that a recoveryis necessary.  A total of six named files can be stored per target port.

To upgrade, first stage the new operating system image(s) on the Local Manager. There are several methods to stage the operating system image. In the below example, the file "DAC-2202_606.s19" in category "OS" is copied from the Uplogix Control Center "ems" to the appliance file archive in the "os" directory.

```
[admin@UplogixLM (port1/3)]# copy ems OS/DAC-2202_606.s19 os DAC606
37,908 bytes read (100%) done
Retrieved 'DAC-2202_606.s19' from 172.30.50.60.
copy succeeded
```

After the copy is complete, the file will appear in the appliance's directory for that port which is viewable using the show directory command.

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

The syntax for the push OS command is:

```
push OS <Version>
```

where Version is the name of the OS, in this case DAC606.

<div class='info'>As part of the push OS command on the Sea Tel driver, the Uplogix automatically detects the type of OS image (ACU, PCU, or CommIF) and upgrades the correct hardware.</div>

```
[admin@UplogixLM (port1/3)]# push OS DAC606
Transferring 37908 bytes
Image version label: MASTER DAC 2202 VER 6.06
Image type: ACU
Locking external port access.
Starting ACU bootloader.
Erase flash.
Erase flash.
Erase flash.
Transferring 864 lines.
....................................................................................... 11%
....................................................................................... 23%
....................................................................................... 46%
....................................................................................... 57%
....................................................................................... 69%
.......................................................................!.!!............ 92%
..............................................................DONE!
Transfer complete.
Hostname     :
Serial Number:
Make         : SeaTel
Model        : DAC 2202
OS Type      : DAC
OS Version   : 6.06
Uptime       :
Push OS succeeded.
```

Note it is normal to see exclamation points (!) or the letter S in the output during the upgrade process. An exclamation point (!) indicates a protected sector the bootloader is not able to write against and an S indicates a slow response from the PCU during transfer.

The PCU is upgraded via the same commands as the ACU.

```
[admin@UplogixLM (port1/3)]# show directory
Type    Version   Name
------- --------- ------------
Config
  Running*
        Current   running-config
        Previous  running-config

  Running-Undo*
        Candidate running-config-undo43433.img

OS
        215       x03-215.s19
        DAC606    DAC-2202_606.s19

* additional archived versions are available. Execute show dir -v

[admin@UplogixLM (port1/3)]# push OS 215
Transferring 19584 bytes
Image version label: xx03 VER 2.15
Image type: PCU
Locking external port access.
Enable PCU bootloader mode.
Normal ACU response
Setup ACU for Remote Module Programming
Checking communication with PCU
PCU responding normally, start Remote Bootloader
Starting PCU bootloader.
PCU bootloader response detected.
PCU bootloader active.
Erase flash.
Transferring 451 lines.
......................................S................................................ 21%
....................................................................................... 44%
....................................................................................... 66%
....................................................................................... 88%
..................................................T
Re-booting ACU
Transfer complete.
Hostname     :
Serial Number:
Make         : SeaTel
Model        : DAC 2202
OS Type      : DAC
OS Version   : 6.06
Uptime       :
Push OS succeeded.
```

The upgrade of the CommIF module utilizes the same push OS command, but in addition to CommIF software, requires specialized bootloader software available from Sea Tel support.  Please contact Sea Tel support by phone (+1 925.798.2399) or email [satcom.concordsupport1@cobham.com](mailto:satcom.concordsupport1@cobham.com) for assistance with CommIF upgrades.

## System Logging Information

When the port is configured as a Sea Tel, the system will log information on DAC status. DAC status is collected with the DAC status monitor command S. The driver captures status information and translates status words into human readable text. The output of the Status messages can be evaluated to customize the Uplogix dashboard display for the Sea Tel port, triangulate a known error condition or forward a syslog message to a network host with the output.

To display the last status response, use the **show faults** command from the port:

```
[admin@UplogixLM (port1/3)]# show faults
PCU Status Bit 0, Satellite out of range, PCU Error, AZ Reference Error, Polang Drive Off, Band Tone Off, Band 13V, AUX is off, Band C, Local-RF 18V, Local Tone Off, No Force NID, FEC-SCPC
```

For more detailed information on system faults, use the verbose option (-v) on the show faults command. The verbose command will display the DAC status words and their translation.

```
[admin@UplogixLM (port1/3)]# show faults -v
   Word 1: 0x40 (01000000)  64 '@'
   Word 2: 0x40 (01000000)  64 '@'
   Word 3: 0x68 (01101000) 104 'h'
   Word 4: 0x48 (01001000)  72 'H'
Remote RF: 0x40 (01000000)  64 '@'
 Local RF: 0x67 (01100111) 103 'g'
    TDisp: 0x00 (00000000)   0 '\u0000'
Satellite out of range, PCU Error, AZ Reference Error, Polang Drive Off, Band Tone Off, Band 13V, AUX is off, Band C, Local-RF 18V, Local Tone Off, No Force NID, FEC-SCPC
```

In addition, the Sea Tel driver can be configured to periodically pull and store this status information. Use the **configure device logging** command to set the Local Manager to automatically collect the faults:

```
[admin@UplogixLM (port1/3)]# config device logging
--- Existing  Values ---
Set the console to use synchronous logging: yes
Set the console to use logging buffered: no
Port syslog forwarding enabled: no
Change these? (y/n) [n]: y
--- Enter New Values ---
Set the console to use synchronous logging (y/n) [y]: y
Set the console to use logging buffered (y/n) [n]: y
Logging level for buffered logging (PIX only) [3]: 
Device buffer polling interval [30]: 
Clear device log buffer on poll (y/n) [n]: n
Log buffer clearing needs to be enabled to use forwarding.
Do you want to commit these changes? (y/n): y
```

To view the stored faults, use the **show device syslog** command:

```
[admin@UplogixLM (port1/3)]# show device syslog
12/09/15 15:28:32.823    Sat Ref Mode, DishScan Disk Error, Polang Drive Off, Band Tone Off, Band 13V, AUX is off, Band C, Local-RF 13V, Local Tone Off, No Force NID, FEC-Auto
```

## Device Execute

The Local Manager provides the ability to interact directly with the DAC without using the **terminal** command via the device execute command. The syntax for the command is:

```
device execute <command>
```

Where <command> is a properly formatted Sea Tel DAC M&C command. When a command is sent to the DAC via device execute, the appliance pulls the running configuration of the DAC. The command then executes and the running configuration is pulled and saved to archive as the current configuration. If the device execute command echoes back a response, it is displayed in the command line. In the example below the response from the Sea Tel is: L1511 @g

```
[admin@UplogixLM (port1/3)]# device execute c1304
beginning pull of running-config
beginning pull of running-config
running-config saved to archive as current.
L1511 @g
```

## DAC Remote Panel Access

The DAC Remote Panel (DacRemP) remote access feature allows the user to utilize Sea Tel's DacRemP program without physical access to the Sea Tel DAC. Use of this feature requires DacRemP software version 1.01 or later. There are two methods to utilize the appliance to populate the data required in DacRemP: Asynchronous modem connection and serial port forwarding. For both methods described, the workstation's TCP/IP loopback (127.0.0.1) interface is utilized. An available local port is presented and configured in DacRemP. The Asynchronous modem connection method is best used in deployments with an Uplogix Control Center whereas the serial port forwarding method requires no Control Center.

### Asynchronous Modem Connection

In the asynchronous modem connection method, the Control Center's CLI applet is utilized to forward a terminal session with the Sea Tel DAC to DacRemP. Once properly authenticated into the Uplogix appliance, the dashboard will display. Navigate to the port in with Sea Tel configured using the port command. 
Then enter into a terminal session with the terminal command as shown in the example below: 

```
Username: admin
Password: *******
Uplogix LMS v5.3 29302 -- Powering Business Uptime
------------------------------------------------------------------------------
Port      Hostname            Status       Con Eth Uptime   Processor    Last
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
1/1  iDirect117440628   Receive Unlocked   *   *   7d 3h    05/00/00    15s
1/2  SeaTel DAC 2202    OK                 *                            1d 2h
1/3  2611-Router        OK                 *       69d 1h   00/00/00
1/4
1/5                     Vessel In Austin   *                            14d 1h
1/6                                        *
1/7
1/8                                        *
PWR  Ambassador4        OK                 *
MDM  iridium            5 Bars             *                            24m 37s
SYS  UplogixLM         OK                 *  *    7d 20h   24/62/43    31s
------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
d=day, h=hour, m=minute, s=second
Active alarms exist. Email notification is suspended while you are logged in.

[admin@UplogixLM]# port 1/2
SeaTel DAC 2202 DAC acu:6.07, pcu:2.51, com:1.12
SeaTel DAC 2202

[admin@UplogixLM (port1/2)]terminal

Press ~[ENTER] to exit.

Connecting ...

Currently running job: rulesMonitor
Press 'x' to exit or 'f' to force (use carefully).
beginning pull of running-config
Pulled 79 configuration lines.
running-config was pulled
running-config saved to archive as current.

Console session started. Press ~[ENTER] to exit.
```

Once the terminal session has started, initiate a forward to DacRemP. On the Terminal menu of the CLI applet select Forward. An open port is selected at random or the user may select an open port. The green colored background of the port number indicates the port is available. A red colored background indicates the port is not available and another port should be selected. Once the port is selected click the Apply button.

![Forward Settings](http://uplogix.com/support/docs/img/lm-user-guide/seatel/seatel9.png)
 
Next, launch the DacRemP software. On the CommPort menu select Properties. Set the IP Address to localhost (127.0.0.1) and enter the Port Number configured in the previous step. In this example the port number is 9100.

![Forward Settings](http://uplogix.com/support/docs/img/lm-user-guide/seatel/seatel10.png)
 
As DacRemP queries the DAC, the commands are displayed and logged in the terminal session window. As long as DacRemP is functioning, the port will not time out. 
 
![Forward Settings](http://uplogix.com/support/docs/img/lm-user-guide/seatel/seatel11.png)

If you would like to interact with the terminal session directly, simply close the port by clicking on the Port Status radio button in DacRemP. The radio button will change from green to red. You can then enter DAC command codes directly in the terminal session window. 

![Forward Settings](http://uplogix.com/support/docs/img/lm-user-guide/seatel/seatel12.png)
 
To reopen the port click on the Port Status radio button again and the connection will be re-established.

### Serial Port Forwarding

The serial port forwarding method is useful for deployments with no Control Center. Follow the instructions in the Feature Guide Serial Port Forwarding available on the Uplogix support website (www.uplogix.com/support) to set up forwarding using PuTTY. 

Authenticate into the Local Manager with the appropriate user name and password. Navigate to the port with the Sea Tel DAC using the port command and enter the terminal command with the forward option: 

```
Username: admin
Password: *******
Uplogix RMOS v4.3 -- Powering Business Uptime
------------------------------------------------------------------------------
Port      Hostname            Status       Con Eth Uptime   Processor    Last
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
1/1  iDirect117440628   Receive Unlocked   *   *   8d 28m    05/00/00    11s
1/2  SeaTel DAC 2202    OK                 *                            1d 23h
1/3  2611-Router        OK                 *       69d 22h   00/00/00
1/4
1/5                     Vessel In Austin   *                            14d 22h
1/6                                        *
1/7
1/8                                        *
PWR  Ambassador4        OK                 *
MDM  iridium            5 Bars             *                            5h 3m
SYS  UplogixLM         OK                 *  *    8d 17h   17/17/19    29s
------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
d=day, h=hour, m=minute, s=second
Active alarms exist. Email notification is suspended while you are logged in.

[admin@UplogixLM]# port 1/2
SeaTel DAC 2202 DAC acu:6.07, pcu:2.51, com:1.12
SeaTel DAC 2202

[admin@UplogixLM (port1/2)]# terminal forward

Press ~[ENTER] to exit.

Connecting ...

beginning pull of running-config
Pulled 79 configuration lines.
running-config was pulled
running-config saved to archive as current.

Console session started. Press ~[ENTER] to exit.
```

Now all interaction with the DAC M&C port is being forward to the workstation's localhost address (127.0.0.1). Next, launch the DacRemP software. On the CommPort menu select Properties. Set the IP Address to localhost (127.0.0.1) and enter the Port Number configured in during port forwarding setup. 

As DacRemP queries the DAC, the commands are displayed and logged in the terminal session window. As long as DacRemP is functioning, the port will not time out. If you would like to interact with the terminal session directly, simply close the port by clicking on the Port Status radio button in DacRemP. The radio button will change from green to red. You can then enter DAC command codes directly in the terminal session window. 

# Custom Rules

## Native Ruleset

This ruleset is to be scheduled as a remotestate monitor on SeaTel DACs. It displays if the SeaTel is has Tracking On or if AGC is below threshold to the dashboard as the status of the DAC.

```
config ruleset seatelNative
description null
rules
seatelAgcBelowThreshold,
exit
exit

config rule seatelAgcBelowThreshold
action writeStatus AGC < Threshold
action alarm -a "AGC Below Threshold"
conditions
remotestate.agcThreshold percent 1.0:remotestate.agc
exit
exit

```

Additionally, this consoleLog rule that looks for "Tracking On", that can be scheduled in addition to the seatelNative ruleset with the command config monitor consoleLog seatelTrackingOn.

```
config rule seatelTrackingOn
action writeStatus Tracking On
conditions
consoleLog.message matches Tracking On
exit
exit
```

## Blockage Zones

The following remotestate rules are an example of blockage zone rules.

The "NearBlockage" rule's azimuth are set slightly larger than the actual blockage zone, and send an alarm when within that azimuth.

The "InBlockage" rule's azimuths correspond with the actual blockage zone.  When in the blockage zone, this rule brings up the out of band connection to report that alarm back to the Control Center.

To schedule the ruleset on your Sea Tel, run the command **config monitor remotestate SeatelBlockageZone**.

```
rule NearBlockageZoneOne
action alarm -a "Approaching Blockage Zone"
conditions
remotestate.azimuthRelative max 67 AND
remotestate.azimuthRelative min 92 AND
remotestate.elevation max 100 AND
remotestate.elevation min 130
exit
exit

rule InBlockageZoneOne
action alarm -a "In Blockage Zone"
action pppCycleHeartbeat
conditions
remotestate.azimuthRelative max 70 AND
remotestate.azimuthRelative min 90 AND
remotestate.elevation max 102 AND
remotestate.elevation min 128 AND
NOT has-run pppCycleHeartbeat :15m
exit
exit

rule NearBlockageZoneTwo
action alarm -a "Approaching Blockage Zone"
conditions
remotestate.azimuthRelative max 150 AND
remotestate.azimuthRelative min 165
exit
exit

rule InBlockageZoneTwo
action alarm -a "In Blockage Zone"
action pppCycleHeartbeat
conditions
remotestate.azimuthRelative max 152 AND
remotestate.azimuthRelative min 163 AND
NOT has-run pppCycleHeartbeat :15m
exit
exit


ruleset SeatelBlockageZone
rules
SeatelBlockageZone1 | SeatelBlockageZone2
exit
exit

ruleset SeatelBlockageZone1
rules
InBlockageZoneOne, NearBlockageZoneOne
exit
exit

ruleset SeatelBlockageZone2
rules
InBlockageZoneTwo, NearBlockageZoneTwo
exit
exit

```

# Rules Engine Variables

When you run a monitor that includes the "remotestate" condition, the following variables are collected:

```
azimuth
relativeAzimuth
crossLevel
agc
agcThreshold
polang
```


# Appendix A: Driver Command Codes

The Uplogix Sea Tel driver utilizes DAC command codes to collect information for monitors and device configuration. Below are the commands the appliance utilizes to query the DAC and PCU.

## Sea Tel Configuration

For DACs with a CommIF module with software version 1.11 or later, the configuration is pulled using the [?ACP command. For DACs with earlier versions of CommIF software or no CommIF module, the configuration is pulled using m commands:

```
Parameter	Command Code
El Trim	mA, mB
Az Trim	mC, mD
Auto Threshold 	mF
El Step Size 	mG
Az Step Size 	mH
Step Integral 	mI
Search Inc  	mJ
Search Limit 	mK
Search Delay 	mL
Sweep Increment	mM
System Type  	mN
Gyro Type   	mO
Polang Type  	mP
24v Polang Offset	mQ
24v Polang Scale	mR
AZ Limit 1   	mS, mT
AZ Limit 2   	mU, mV
Polang Tx Type 	mW
AZ Limit3	mY, mZ
AZ Limit4	m[, m\
AZ Limit5	m], m^
AZ Limit6	m_, m`
Lat      	mb, mc
Lat ns     	md
Lon      	me, mf
Lon ew     	mg
SAT      	mh, mi
Sat ew     	mj
Hdg      	mk, ml
R Hdg     	mm, mn
THRS      	mo, mp
Freq / MHz   	mq, mr
Baud / KHz   	ms, mt
FEC Tone Volt 	mu
POL SEL	mv
AGC      	mw, mx
Ext AGC/Modem 	my, mz
Remote POL   	m{, m|
Target NID   	m}, m~
KuDisp     	mâ‚¬
TDisp     	mâŠ”
AZ Limit7 / Pol5 Offset	m,, mÆ’
AZ Limit8	mâ€ž, mâ€¦
EL Limit12   	mâ€ 
EL Limit34   	mâ€¡
EL Limit56   	mË†
EL Limit78   	mâ€°
SatSkew	mÅ 
IP Address	[I
Netmask	[N
Gateway	[G
TCP-0 Port On Off	[0
TCP-1 Port On Off	[1
TCP-2 Port (Open AMIP) On Off	[2
UDP Port On Off	[U
M&C Baud Rate On Off	[C
NMEA A Baud Rate On Off	[A
NMEA B Baud Rate On Off	[B
LO Band 1	[D1
LO Band 2	[D2
LO Band 3	[D3
LO Band 4	[D4
NMEA Heading ID	[H
Web (HTTP) On Off	[T
Enabled Mask	[O
Secured Mask	[Q
Pedestal Type	n0
CL Loop Gain	n1
LV Loop Gain	n2
AZ Loop Gain	n3
CL Tilt Trim	n4
LV Tilt Trim	n5
Home Flag Trim	n6
DishScan Setup	n7
Scan Rate	n8
Error Flags	n9
System ID	nA
```

## Sea Tel Remote State Monitor

```
Parameter	Command Code
Heading	H
Azimuth	P
Relative Azimuth	H
Elevation	P
Cross Level	P
AGC	%
AGC Threshold	u
Polarity Angle	u
Sea Tel GPS Monitor
Parameter	Command Code
Latitude	?@
Longitude	?@
Cross Level	P
Heading	H
Elevation	P
# of Satellites	?@
```