<!-- 5.4 -->

If you encounter a situation in which a managed device suffers a hardware failure or loses its startup configuration, it is possible to quickly replace that device by installing a new "bare-metal" device. The Local Manager will automatically detect and attempt to restore the new router to the operational state of the previous router.

> For this document, a **router** will be used as an example device.

# Overview

Bare Metal Restore (BMR) is an automated recovery feature built into the Cisco advanced driver. As the Local Manager interacts with the router, it is continuously trying to detect device state. If it detects a bad state (loss of config, stuck in ROMMON mode), it will attempt to recover the router. 

Recovery actions may include:

* Issuing a command to boot the router
* Issuing a **boot tftp** command in case there is a problem with the device's storage
* Push down the current startup-config
* Push down the current OS image

**To the Local Manager, there is no functional difference between a router that has lost its config and a new router with no configuration on it.**

# Requirements

Before you can use BMR, the following requirements must be met:

1. The port on which the BMR will be performed must be initialized correctly (make/model set)
2. The Local Manager must have previously pulled a startup-config and marked it as *current* **OR** the user has copied a startup-config to the Local Manager manually and marked it as *current*
3. To restore an OS, the Local Manager must have previously pulled an OS image and marked it as **current** the user has copied an OS image to the Local Manager manually and marked it as *current*
4. A scheduled job or monitor must be running (device state is detected only during automated functions). A chassis monitor is scheduled to run every 30 seconds by default.

# Removing the Old Device

If the old router has failed and is no longer responding on its console port, you can simply unplug it and remove it from the rack.

If the Local Manager was actively managing the router, it will be generating alarms indicating a communication problem. These are fine and can be ignored during the hardware replacement. 

# Installing the New Device

Rack the new router connect its console port to the Local Manager. Apply power and allow it to boot. 

> If you will be using the Local Manager to push down an OS image, connect the new router to the local network or directly to the associated dedicated Ethernet port on the Local Manager (Uplogix 5000 only).

## Booting into ROMMON Mode

A new router should come with an operating system already installed. However, in the rare case that it boots into ROMMON mode, the Local Manager will attempt to restore the last OS image it pulled (from the previous device).

## Enter Config Mode?

A new router should boot up without a startup config and prompt the user to enter configuration mode. 

```
Would you like to enter the initial configuration dialog? [yes/no]: 
% Please answer 'yes' or 'no'.
Would you like to enter the initial configuration dialog? [yes/no]: terminal length 0
% Please answer 'yes' or 'no'.
Would you like to enter the initial configuration dialog? [yes/no]: 


Press RETURN to get started!


00:00:07: %LINS (tm) C2600 Software (C2600-I-M), Version 12.2(26), RELEASE SOFTWARE (fc2)
Copyright (c) 1986-2004 by cisco Systems, Inc.
Compiled Sat 31-Jul-04 04:57 by eaarmas
00:00:29: %SNMP-5-COLDSTART: SNMP agent on host Router is undergoing a cold start
```

Since the Local Manager is still trying to manage the router, it will detect this message and notice that something is wrong. In the snippet above, notice how it sends the **terminal length 0** command while being prompted for something else. This piece triggers the recovery process. 

The Local Manager then attempts to push down the *current* startup-config (from the previous device or manually copied over).

> The copy commands used will differ from router to router.

```
Router#copy xmodem: flash0:/staging-startup-config
			**** WARNING ****
x/ymodem is a slow transfer protocol limited to the current speed
settings of the auxiliary/console ports. The use of the auxilary
port for this download is strongly recommended.
During the course of the download no exec input/output will be
available.
			---- ******* ----


Proceed? [confirm]y
Source filename []? staging-startup-config
Destination filename [staging-startup-config]? staging-startup-config
Use crc block checksumming? [confirm]y
Max Retry Count [10]: 
Perform image validation checks? [confirm]n
Xmodem download using crc checksumming with NO image validation
Continue? [confirm]y
Ready to receive file...........C
5248 bytes copied in 28.304 secs (185 bytes/sec)

Router#

Router#copy flash0:/staging-startup-config startup-config
Destination filename [startup-config]? 
[OK]
5248 bytes copied in 2.668 secs (1967 bytes/sec)

Router#delete flash0:/staging-startup-config
Delete filename [staging-startup-config]? 
Delete flash0:/staging-startup-config? [confirm]
Router#
Router#
Router#terminal length 0
Router#show bootvar | include CONFIG_FILE
             ^
% Invalid input detected at '^' marker.

Router#verify /MD5 nvram:startup-config
..Done!
verify /md5 (nvram:startup-config) = 6b61400490cfc9788148239053055bac


Router#config term
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#config-register 0x2102
Router(config)#exit
Router#
%Error opening tftp://255.255.255.255/router-confg (Timed out)
Router#reload
```

## Router or Switch Hostname

If the new device has already booted and a user has bypassed the configuration mode prompt, the Local Manager can key off the default hostname of *Router* or *Switch*. In that case, the Local Manager will try pushing down the startup-config as shown in the previous example.

# Returning to Normal

Once the startup-config has been pushed to the new router, the Local Manager will resume normal management and continue running its scheduled jobs and monitors.

If [OS Policies](/docs/control-center-user-guide/managing-local-managers/os-policies) have been applied to the deployment AND the new router came with an out-of-date IOS version, it will be upgraded to the predetermined version.

> Once the router is upgraded, the startup-config will be pushed again in case some elements of the config required the IOS version specified in OS Policies.

If OS Policies is not enabled, the OS file on the new router will be archived to the Local Manager the next time the Pull OS job runs (by default, every 14 days). You can run the job manually with the **pull os** command. Alternately, you can use the **push os** command to load the previous IOS image onto the router, especially if the startup-config depends on features from a particular version of IOS.