<!-- 5.4 -->

Use the **push** command to write a saved configuration to a device.

Whether you write the entire configuration or make incremental changes, the procedure is:

1. Pull the current running configuration from the device by logging into the device with the **terminal** command.
2. Verify that the configuration file you intend to push is the correct file.
3. Push the file using either the **push startup-config** or the **push running-config** command. 
 
The Local Manager will pull the configuration before and after the push operation, so the change can be undone if necessary.

Use **push startup-config** to write the entire configuration (e.g., replacing a device). For the case of a device with a VLAN database, also use **push vlan** to restore the VLAN database (vlan.dat) file.

Use the **push running-config** command to make incremental changes. In the example below, the running-config candidate file contains only one line; when this running-config file is pushed to the device, only its hostname will be changed.

First, log into the device with the **terminal** command. The Local Manager automatically pulls the current running-config so it can track changes made during the terminal session, which are required for the rollback feature and device change logging. 

```
[admin@UplogixLM (port 1/1)]# terminal

Press ~[ENTER] to exit
Connecting ...
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.

Console session started.
```

The **show running-config** command displays the device's current configuration. Some information has been removed from the command output.

```
XYZ-CORE# show run
Building configuration...
Current configuration : 750 bytes
!
version 12.2
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service tcp-small-servers
!
hostname XYZ-CORE
!
logging buffered 4096 debugging
no logging console

[output removed]

XYZ-CORE#
Console session ended.

Disconnecting ...

Logging out of device...
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
```

The Local Manager pulls the running configuration again as the terminal session ends.

Using the **show running-config** candidate command, view the running configuration file that you will push to the device.

```
[dsmith@UplogixLM (port1/1)]# show running-config candidate
hostname foo
```

This running configuration file will only change the device hostname. To push this configuration to the device, use the **push running-config candidate** command.

```
[admin@UplogixLM (port1/1)]# push running-config candidate
Retrieving running-config from device ...
Complete. running-config pulled.

Copying running-config to device.

Transferring via XModem. (Attempt 1)
Initiating file transfer
Transferring file ...

Sent running-config at 133 B/s.

File running-config was transferred to the device successfully via XModem.
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
runningConfig downloaded to device.
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
```

When the file transfer is complete, view the new running configuration using the **show running-config current** command. Some information has been removed from the command output.

```
[admin@UplogixLM (port1/1)]# show running-config current
!
version 12.2
no service pad
service timestamps debug datetime msec
service timestamps log datetime msec
Managing Devices
User Guide for Local Managers 115
no service password-encryption
service tcp-small-servers
!
hostname foo
!
logging buffered 4096 debugging
no logging console
[output removed]
```