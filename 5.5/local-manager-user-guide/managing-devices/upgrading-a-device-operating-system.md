<!-- 5.4 -->

Before you start, obtain the appropriate OS image from the manufacturer of the device to be upgraded.

To transfer the file using FTP, TFTP, or SFTP, Ethernet connectivity to the managed device is required; xmodem or ymodem may be used with serial connections when supported by the managed device.

To transfer an OS image to the Local Manager, navigate to the port that is connected to the managed device and execute the **copy** command:

```
copy [scp|ftp] "username@server:fileName" os [candidate|current]
```

For example, to copy a new Cisco switch OS from a server to the Local Manager using the SCP protocol:

```
[admin@UplogixLM (port1/1)]# copy scp dsmith@203.0.113.11:c3560-12.3t.bin os candidate
```

Enter the show settings command to determine the current file transfer preference settings for this port. To change the current settings, use the **config settings** command.

After configuring OS upgrade settings, the upgrade can be performed. The image previously downloaded to the Local Manager has been assigned to the candidate slot, which means it has not yet been successfully deployed to your specific device.

To begin the upgrade, enter or schedule the **push os candidate** command from the appropriate port resource. The Local Manager first attempts to transfer the image using the primary method.  If that fails, the alternative method is used. When the transfer is complete, the device may automatically reboot if the Local Manager port settings are configured to include this behavior.  The Local Manager monitors and saves the Power On Self Test (POST) log messages and reports if the upgrade is successful. You may manually schedule a reboot for later, but in this case the automated validation will not be performed.

```
[admin@UplogixLM (port2/1)]# push os candidate
System image file is "flash0:/c2951-universalk9-mz.SPA.151-4.M.bin"
6 interfaces and 1 types found.
Information logged Before Upgrade
There are no outlet mappings for this device.
Hostname : Aus3-router
Serial Number: FT2TX19AKZR
Make : cisco
Model : CISCO2951/K9
OS Type : IOS
OS Version : 15.1(4)M
Uptime : 2 weeks, 2 days, 4 hours, 58 minutes
Device Image Verified.
Initiating file transfer
Sending c2951-universalk9-mz.SPA.151-3.T1.bin to 192.0.2.2:
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
TFTP download of c2951-universalk9-mz.SPA.151-3.T1.bin succeeded.
Verified: flash0:c2951-universalk9-mz.SPA.151-3.T1.bin
Retrieving running-config from device ...
Complete. running-config pulled.
Retrieving running-config from device ...
Complete. running-config pulled.
Issuing 'reload'
Reading post
Bootstrap posted
CISCO2951/K9 platform with 2621440 Kbytes of main memory
.Image decompressing
Image decompressed

Device loaded

Post complete.
Hostname : Aus3-router
Serial Number: FT2TX19AKZR
Make : cisco
Model : CISCO2951/K9
OS Type : IOS
OS Version : 15.1(3)T1
Uptime : 0 minutes
6 interfaces and 1 types found.
Push OS succeeded.
```