<!-- 5.4 -->

Schedules jobs to execute automatically. Choose from available jobs listed in the help text when using the config schedule command.

# Command availability 

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, ppp, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config schedule <time> <"jobname" ["job args"]>
```

**time** can be of one of the following formats:

Calendar-based using cron notation:

**<[-m 0-59] [-h 0-23] [-D 1-31] [-M 1-12] [-W 0-6]> [-d delay]>**
- -m {0..59} minute range
- -h {0..23} hour range
- -D {1..31} day of the month
- -M {1..12} month range
- -W {0..6} - day of the week; 0 is Sunday.
- -d <"delay"> delay in seconds between 2 consecutive executions of the job


Interval-based: 

**[-s startTime] [-e endTime] <-d delay>**
- -d <"delay"> delay in seconds between 2 consecutive executions of the job
- -e <end time> end time after which the job is removed from the scheduler
- -s <start time> start time for the job

One time: 

- -o <one time> - the one time at which the job should run. 

Values for **<start time>**, **<end time>**, and **<one time>** are in **MM/dd/yy-hh:mm:ss** format.

**jobname** - The command to run followed by its arguments. Job names require no spaces and use special names.

The jobs that can be scheduled depend on the device. The following jobs are defined:

-   **assimilate** - Assimilate a device. 
- 	**certify** - Copies working directory contents to certified (Alcatel).
- 	**clearCounters** - Clears all interface counters.
- 	**clearServiceModule** - Clears the service module.
- 	**deviceInfo** - Collects device serial number, make, model, and OS information.
- 	**interfaceCycle** - Cycles the interface specified.
- 	**interfaceOff** - Turns off the interface specified.
- 	**interfaceOn** - Turns on the interface specified.
- 	**pppOff** - Turn PPP off.
- 	**pppOn** - Turn PPP on.
- 	**pullOS** - Copies an OS image from the device to the system.
- 	**pullRunningConfig** - Copies a running config file from the specified device to the system.
- 	**pullStartupConfig** - Copies a startup config file from the specified device to the system.
- 	**pushOS** - Push an OS image to the specified device.
- 	**pushRunningConfig** - Push a running config to the specified device.
- 	**pushStartupConfig** - Push a startup config to the specified device.
- 	**reboot** - Reboot the device connected to this port. 
- 	**rebootAll** - Reboot the stack to which this device belongs (Alcatel).
- 	**rebootWorking** - Reboot the device from the working configuration (Alcatel).
- 	**recoverPassword** - Forces restore of last known startup.
- 	**restore** - Copies certified directory contents to working (Alcatel)
- 	**showTech** - Collect tech support information from the specified device.
- 	**writememory** - Saves running config. 

# Usage 

```
[admin@UplogixLM (port1/1)]# config schedule -s 01/03/14-10:30:00 -e 02/03/14-10:29:59 -d 30 deviceInfo
```

executes deviceInfo every 30 seconds between Jan 3 and Feb 3 2014 

```
[admin@UplogixLM (port1/1)]# config schedule -M 3 -m 30 clearCounters
```

executes clear counters every half hour in March.

# In the Uplogix web interface

**Schedule > schedule task button** - all devices and system that match the selected filter

**Inventory > Local Manager page > schedule button** - specific to this system

**Inventory > Local Manager page > port detail > schedule button** - specific to this device

# History 

3.4 - Added actions that can be scheduled on Alcatel devices: certify, restore, rebootWorking, rebootAll.

# Related commands 

- **config removejob**
- **show schedules**
