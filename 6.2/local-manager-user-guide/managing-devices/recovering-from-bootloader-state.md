<!-- 5.4 -->

Local Managers can recover devices that have entered a boot loader state such as Cisco's ROMmon state. While the process varies among vendors and models, the Local Manager delivers standardized operations that require low-level boot loader and operating system configuration recovery steps in an efficient, rapid manner.

The recovery process is automatic and does not require any immediate user attention to initiate or complete.

> Some managed devices may require additional setup. See [Customizing Cisco ROMmon Recovery](http://uplogix.com/docs/local-manager-user-guide/advanced-features/customizing-cisco-rommon-recovery).

You must have copies of the device OS and startup configuration files in order to recover from ROMmon.

The **config init** command schedules periodic collection of these files. The OS files are transferred using the FTP and TFTP protocols, so you must have a working network connection from the Local Manager's management Ethernet interface to an Ethernet interface on the device in question.

If the device's operating system does not offer this ability, the files can be obtained from the vendor and stored on the Local Manager in the event they are needed.

After the **pull os** command is successful, the Local Manager will have a copy of the device's OS image stored locally. The stored image is relevant only for the device connected to the Local Manager's console port. If you prefer to use a previously collected OS file from one port for another port, reference the copy command.

The following is a **pull os** command example:

```
[admin@UplogixLM]# port 2/2
AustinR1-SRE cisco CISCO2921/K9 IOS 15.1(4)M
			 Cisco2921

[admin@UplogixLM (port2/2)]# pull os
Starting pull of Cisco IOS Image
System image file is "flash:/c2900-universalk9-mz.SPA.151-4.M.bin"
Backing up os file: flash:c2900-universalk9-mz.SPA.151-4.M.bin
Transferring file via FTP

Writing scratch/temp.file
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
70542428 bytes copied in 29.516 secs (2389972 bytes/sec)

AustinR1-SRE#
FTP Transfer complete

[admin@UplogixLM (port2/2)]# show directory
Type Version Name
------- --------- ------------
Config
	Running
		current running-config

	Startup
		current startup-config
OS
		current c2900-universalk9-mz.SPA.151-4.M.bin
```

In this example, if the Local Manager later detects that the Cisco 2921 is in ROMmon mode, it immediately attempts a recovery. If it finds a bad or missing OS image, the Local Manager will use the stored current OS image as part of its recovery process.

The configuration file used to cold-start a network device will also be necessary.

Retrieve the startup configuration using the **pull startup-config** command to maintain a copy locally for these and other operational recovery procedures. As above, you can also schedule the Local Manager to automatically gather this information as often as is practical.

These files are automatically scheduled when using the **config init** command in setting up a new supported device.