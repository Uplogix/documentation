<!-- 5.4 -->

# Overview

Local Managers can use an external power controller in the management and recovery of network devices. If the power controller has not been configured, it must be initialized before power features will be available on port resources.

# New for 5.4 

In previous versions of LMS, the power controller had a separate, fixed port (1/6 on the Uplogix 500/5000). As of 5.4, all serial ports on the Local Manager can now be configured as power controllers. As a result, the **powercontroller** resource and related command have been removed.

# Initializing a Port

The initialization process is similar to initializing a port. Only the make and OS are required. The following makes are currently supported:

 - APC
 - Avocent
 - BayTech
 - Lantronix
 - ServerTech

Use the **config init** command to begin initialization of the power controller. Once the Local Manager establishes a connection and verifies the login credentials, it will query to power controller to retrieve the names of the power outlets. If successful, it will then prompt you to map power outlets to ports on the Local Manager.

```
[super@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: Austin Rack 123 Power
make [native]: servertech
model: 
os: sentry
os version: 
management IP: 
Configure dedicated Ethernet port? (y/n) [n]: n 
console username: admn
console password: ****
confirm password: ****
Serial Bit Rate [9600]: 
Serial Data Bit [8]: 
Serial Parity [none]: 
Serial Stop Bit [1]: 
Serial Flow Control [none]: 
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
Retrieving outlet names.  Please wait...
Outlet names retrieved.
Would you like to add a new mapping? (y/n) [n]: y
Outlet: A1
Interface: port1/1
Would you like to add a new mapping? (y/n) [n]: y
Outlet: A2
Interface: port1/2
Would you like to add a new mapping? (y/n) [n]: n
Scheduling default jobs
Testing job rulesMonitor
Job rulesMonitor was successful
Job rulesMonitor was scheduled
Testing job rulesMonitor
Job rulesMonitor was successful
Job rulesMonitor was scheduled
```

After initialization, you can return to the power controller port and edit its settings with the following commands:

**config authentication**: Configure the information that the Local Manager uses to log into the power controller.

| Make | Default Credentials
|-|-|
| ServerTech | admn / admn
| Lantronix | sysadmin / pass
| APC | apc / apc
| Baytech | admin / baytech
| Avocent | admin / avocent, root / linux

**config outlets**: Specify the outlets to which managed devices are connected. Use this command to add/remove outlet mappings.

**config serial**: Specify the serial settings for the power controller.

**config info**: Modify information about the power controller such as make, model, OS, and management IP address.

Each of these config commands has a corresponding **show** command to view what is currently configured.

# Controlling Power

There are three commands that can be used to control power to a managed device.

## By Outlet Name, from the Power Controller Port

You can turn outlets off and on using the **off** and **on** commands from the power controller port. These commands bypass any management of the device connected to the outlet.

```
[super@UplogixLM (port1/4)]# off A1
Powering off port1/4 outlet(s) [A1]
Powering off outlet(s) [A1]

[super@UplogixLM (port1/4)]# on A1
Powering on port1/4 outlet(s) [A1]
Powering on outlet(s) [A1]
```

> There is no individual command to cycle power (i.e., to turn off and on a particular outlet). To power cycle a device, use the **power** command.

## By Outlet Mapping, from the Power Controller Port

You can use the **power** command to modify all outlets mapped to a specific port. This is often used for managed devices with multiple power supplies. Instead of issuing **off A1** and **off A2**, you can simply issue **power port 1/2 off** if the outlets have been mapped correctly.

```
[super@UplogixLM (port1/4)]# power port 1/2 off
1/4:  Powering off port1/4 outlet(s) [A2]
1/4:  Powering off outlet(s) [A2]
1/4:  CTS was active.
```

The message *CTS was active* is displayed to relay the state of the managed device's serial port prior to powering off.

## By Outlet Mapping, from a Port Resource

If outlets have been mapped to a port, you can use the **power** command to modify the power state of that port. This is similar to the previous **power** command, except that it is not necessary (nor supported) to specify the port to perform the power operation on. 

```
[super@UplogixLM (port1/2)]# power on
1/4:  Powering on port1/4 outlet(s) [A2]
1/4:  Powering on outlet(s) [A2]
```

# Cycling Power

At minimum, cycling power involves turning power off and back on. For ports with native or enhanced drivers, the **power** command will only perform those operations.

```
[super@UplogixLM (port1/3)]# power cycle
1/4:  Powering off port1/4 outlet(s) [A3]
1/4:  Powering off outlet(s) [A3]
1/4:  Powering on port1/4 outlet(s) [A3]
1/4:  Powering on outlet(s) [A3]
```

If a port has been configured with an advanced driver, the **power** command may include a serial connection check and, if supported, a capture of the managed device's POST output.

Here is an example from a Cisco router:

```
[super@UplogixLM (port1/2)]# port 1/1
AUS-CORE2 cisco 2610 IOS 12.2(26)
          Cisco Router

[super@UplogixLM (port1/1)]# power cycle
1/4:  Powering off port1/4 outlet(s) [A1]
1/4:  Powering off outlet(s) [A1]
1/4:  DSR was active.
1/4:  CTS was active.
1/1:  Reading post
1/4:  Powering on port1/4 outlet(s) [A1]
1/4:  Powering on outlet(s) [A1]
1/1:  Bootstrap posted
1/1:  C2600 platform with 24576 Kbytes of main memory
1/1:  Image decompressing
1/1:  Image decompressed
1/1:  Started

1/1:  Post complete.
Serial link (DSR) is active.
Serial link (CTS) is active.
getting device uptime
Hostname     : AUS-CORE2
Serial Number: JAB030608LC
Make         : cisco
Model        : 2610
OS Type      : IOS
OS Version   : 12.2(26)
Uptime       : 0 minutes
System image file is "flash:/c2600-i-mz.122-26.bin"

start time was    : Thu Jan 12 14:47:06 UTC 2017
start time is now : Thu Jan 12 14:57:45 UTC 2017
```

The POST output is saved on the filesystem:

```
[super@UplogixLM (port1/1)]# show dir -v
All times shown in UTC.

Type     Version    Size        Date          Name
-------  ---------  ----------  ------------  ------------
Config
    Running
         current    1021        Dec  5 13:25  running-config

    Startup
         current    1021        Dec  5 13:25  startup-config

OS
         current    5569272     Dec  5 13:26  c2600-i-mz.122-26.bin

Post
         current    2379        Jan 12 14:57  readPost
```