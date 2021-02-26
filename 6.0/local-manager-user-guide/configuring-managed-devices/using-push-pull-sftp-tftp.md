<!-- 5.4 -->

# Overview

Local Manager device drivers have functionality that enables manual and automatic transfer of configuration and OS files between the Local Manager and the managed device using Secure File Transfer Protocol (SFTP) or Trivial File Transfer Protocol (TFTP).

The pull SFTP and pull TFTP features are used to transfer files from the managed device to the Local Manager. The push SFTP and push TFTP features are used to transfer files from the Local Manager to the managed device. These features can be initiated as a CLI command, a scheduled job, or an action in a rule.

The SFTP command generates a temporary unique password to authenticate the SFTP transfer. Remember to allow outbound SSH connections from the deviceâ€™s console port since it is the underlying transport for SFTP. For example, on a Cisco device you should include the configuration:

* line con 0
* transport output ssh

There are several instances when it would be appropriate to apply the pull/push SFTP or TFTP feature, such as:

* Schedule pull SFTP and pull TFTP jobs for a device configured with the Enhanced Native device driver to regularly backup startup and running configuration files to the Local Manager file system for that device.
* Back up OS image files from the managed device to the Local Manager.
* Back up any file from a managed device to the Local Manager.
* Automatically restore a golden configuration file to the managed device when certain conditions are met on the managed device using a monitor and the rules engine.
* Locally stage and download managed device OS files from the Local Manager.â€ƒ

To use pull and push SFTP or TFTP, a user must have the following privileges: 

- **pull file** â€“ The define and initiate command to copy a file from the managed device to the Local Manager.
- **push file** â€“ The define and initiate command to copy a file to the managed device from the Local Manager.

# Pull TFTP or SFTP Usage

Use the following command at the Local Manager port prompt to transfer a file from a managed device to the Local Manager:

```
pull tftp [dedicated] <â€œremote commandâ€> <xferFileName> <type> [version]
```

```
pull sftp [options] "<remote command>" <type> [version]
```

## Dedicated (TFTP)

An optional parameter that can be added to specify the use of a dedicated Ethernet connection between the Local Manager and managed device for the file transfer.

## Options (SFTP)

Since SFTP transfers have more options, the *dedicated* and *xferFileName* arguments of the Pull TFTP command have been combined into a single options statement.

* **-cprompt matchText** - Confirmation prompt to respond to
* **-dedicated** - Forces use of dedicated Ethernet
* **-file xferFileName** - The name of the file being pulled/transferred from the managed device to the Local Manager.
* **-pprompt matchText** - Password prompt to respond to 

## Remote Command

The copy command that should be issued at the CLI of the managed device to copy a file over to the Local Manager from the managed device. This command string can also include embedded escape sequences such as \r, which are helpful when the managed device command involves a command dialogue rather than a single command.

## xferFileName

The name of the file being pulled/transferred from the managed device to the Local Manager.

The transfer filename must be unique across all ports in the Local Manager. For example, if there are two enhanced native ports managing the same kind of device, the transfer filename must be different for each port.

## type

Any of the local filesystem types: os, running-config, startup-config, show-tech, or post

## version

Any of the local filesystem versions: candidate, current, previous, customVersion

## Variables

For SFTP transfers, additional variable information is required. The SFTP variables are used in the deviceâ€™s syntax to place macros instead of hard coding names and addresses. The Local Manager will replace these at runtime with appropriate substitutes:

 - **${user}**: The macro to insert the port username into the deviceâ€™s file transfer command.
 - **${pass}**: The macro to insert the temporary password available for file transfer to that port.
 - **${path}**: Temporary file name for transfer to the Local Manager.
 - **${ip}**: IP address on Uplogix to transfer the file to. Could be subinterface, dedicated or management.

## TFTP Example

The first example demonstrates pulling the startup-config from the Extreme switch. Note the use of the \x22 escape sequence in the command that is used to put the VR-Mgmt parameter in double quotes. Note that 192.0.2.151 is the IP address of the Local Manager.

```
[admin@UplogixLM (port1/1)]# pull tftp "upload log 192.0.2.151 vr \x22VR-Mgmt\x22 Extreme150Log chronological" Extreme150Log show-tech
Pull showTech/current ...
TFTP server at 192.0.2.151:69
Executing: upload log 192.0.2.151 vr \"VR-Mgmt\" Extreme150Log chronological
Received Extreme150Log (47,156 bytes)
MD5: cd607a15b7472c37ea9c8d968ca626a4
```

The next example below demonstrates pulling the running-config from the Extreme switch:

```
[admin@UplogixLM (port1/1)]# pull tftp "upload configuration 192.0.2.151 
x150RunningConfig" x150RunningConfig running-config current
Pull runningConfig/current ...
TFTP server at 192.0.2.151:69
Executing: upload configuration 192.0.2.151 x150RunningConfig
Received x150RunningConfig (11,770 bytes)
MD5: dcd44a8490522671addebcd84fc0fdfa
```

The second example demonstrates chaining two commands together with the \r escape sequence (for a carriage return) between the commands in order to issue a show tech on the Extreme switch and then copy the resulting file to the Local Manager as the current Tech file.

```
[admin@UplogixLM (port1/1)]# pull tftp "show tech all logto file \r tftp put 192.0.2.151 internal-memory show_tech.log.gz" show_tech.log.gz show-tech current
Pull showTech/current ...
TFTP server at 192.0.2.151:69
Executing: show tech all logto file \r tftp put 192.0.2.151 internal-memory 
show_tech.log.gz
Received show_tech.log.gz (16,786 bytes)
MD5: 8c36d5aeacf34b9cdb4a75d0467048c2
Issue the show directory command to see files pulled from the managed device.
[admin@UplogixLM (port1/1)]# show directory
Type		Version				Name
-------	----------			------------
Config
Running
Current				x150RunningConfig
Startup
Current				x150StartupConfig
OS
Candidate			summitX-12.4.5.3.xos
Tech*
Current				Extreme150Log
Previous				show_tech.log.gz
* Additional archived versions are available. Execute show dir -v
```

## SFTP Example

This example demonstrates pulling the self-signed certificate from a Cisco router using SFTP. Note the use of the variables to populate the routerâ€™s parameters with the Local Managerâ€™s information. Since the router needs a carriage return to execute, it is represented with a â€˜**\r**â€™ at the end of the remote command. We will place the certificate in a named OS object â€œCertâ€ since it is a binary file.

```
[admin@UplogixLM (port1/1)]# pull sftp -file IOS-Self-Sig#3737.cer "copy nvram:IOS-Self-Sig#3737.cer scp:\r${ip}\r${user}\r${path}\r${pass}\r" os  Cert

Pull os/custom ...
SFTP/SCP service at 192.0.2.220:22
Executing: copy nvram:IOS-Self-Sig#3737.cer scp:\r${ip}\r${user}\r${path}\r${pass}\r
Responding to password prompt
SFTP/SCP started
SFTP/SCP done
Transfer complete
```

The next example demonstrates pulling a text file from the routerâ€™s flash that maintains DHCP address information:

```
[admin@UplogixLM (port1/1)]# pull sftp -file dhcp "copy flash:dhcp-bindings.txt scp:\r${ip}\r${user}\r${path}\r${pass}\r" startup-config dhcp
Waiting for another job to complete
Pull startupConfig/custom ...
SFTP/SCP service at 203.0.1130.100:22
Executing: copy flash:dhcp-bindings.txt scp:\r${ip}\r${user}\r${path}\r${pass}\r
Waiting for SFTP/SCP to start ....Responding to password prompt
SFTP/SCP started
SFTP/SCP done
Transfer complete
```

Issue the show directory command to see files pulled from the managed device.

```
[admin@UplogixLM (port1/1)]# show directory
Type		Version				Name
-------	----------			------------
Config
Running
Current				x150RunningConfig
Startup
Current				x150StartupConfig
dhcp       			dhcp
OS
Candidate			summitX-12.4.5.3.xos
Cert       			IOS-Self-Sig#3737.cer
Tech*
Current				Extreme150Log
Previous				show_tech.log.gz
```

Issue the **show startup dhcp** command to see content of text files:

```
[admin@UplogixLM (port1/1)]# show startup dhcp
*time* Dec 30 2013 04:17 PM
*version* 4
!IP address     Type  Hardware address   Lease expiration       VRF
203.0.113.169    id    0124.ab81.e070.73  Dec 31 2013 04:03 PM
203.0.113.170    id    0144.4c0c.c049.2e  Dec 31 2013 01:05 PM
203.0.113.171    id    0100.f4b9.6098.c2  Dec 31 2013 03:54 PM
203.0.113.172    id    0130.10e4.84fc.a7  Dec 31 2013 11:02 AM
203.0.113.173    1     fe7b.6609.2770     Dec 31 2013 10:58 AM
```

# Push TFTP or SFTP Usage

Use the following command at the Local Manager port prompt to transfer a file from the Local Manager file system to a managed device:

```
push tftp [dedicated] "<remoteCmd>" <xferFileName> <type> [version]
push sftp [options] "<remoteCmd>" <type> [version]
```

## Dedicated (TFTP)

Include this information when you want to move files over a dedicated Ethernet link between the Local Manager and managed device rather than using the management Ethernet interface (i.e. moving files over the LAN).
 
## Options (SFTP)

Since SFTP transfers have more options, the *dedicated* and *xferFileName* arguments of the Pull TFTP command have been combined into a single options statement.

* **-cprompt matchText** - Confirmation prompt to respond to
* **-dedicated** - Forces use of dedicated Ethernet
* **-file xferFileName** - The name of the file being pulled/transferred from the managed device to the Local Manager.
* **-pprompt matchText** - Password prompt to respond to 

## Remote Command

The copy command that is issued at the CLI of the managed device to copy a file from the Local Manager to the managed device. This command string can also include embedded escape sequences such as \r, which are helpful when the managed device command involves a command dialogue rather than a single command. Refer to the ASCII Escape Sequences section below for more information about escape sequences.

## xferFileName

The name of the file being pulled/transferred from the managed device to the Local Manager.

The transfer filename must be unique across all ports in the Local Manager. For example, if there are two enhanced native ports managing the same kind of device, the transfer filename must be different for each port.

## type

Any of the local filesystem types: os, running-config, startup-config, show-tech, or post

## version

Any of the local filesystem versions: candidate, current, previous, customVersion

## Variables

For SFTP transfers, additional variable information is required. The SFTP variables are used in the deviceâ€™s syntax to place macros instead of hard coding names and addresses. The Local Manager will replace these at runtime with appropriate substitutes:

 - **${user}**: The macro to insert the port username into the deviceâ€™s file transfer command.
 - **${pass}**: The macro to insert the temporary password available for file transfer to that port.
 - **${path}**: Temporary file name for transfer to the Local Manager.
 - **${ip}**: IP address on Uplogix to transfer the file to. Could be subinterface, dedicated or management.

## TFTP Example

The first example chains two commands together (with the **\r** escape sequence for a carriage return between the commands) in order to push a golden running-config file from the Local Manager file system to an Extreme switch and then load it to the running configuration.

Note that 192.0.2.151 is the IP address of the Local Manager.

```
[admin@UplogixLM (port1/1)]# push tftp "tftp get 192.0.2.151 x150RunningConfig.xsf \r load script x150RunningConfig.xsf" x150RunningConfig.xsf running-config Golden
Push runningConfig/custom ...
TFTP server at 192.0.2.151:69
Executing: tftp get 192.0.2.151 x150RunningConfig.xsf \r load script x150RunningConfig.xsf
Transfered x150RunningConfig.xsf
```

The second example demonstrates pushing a candidate OS file to an Extreme switch:

```
[admin@UplogixLM (port1/1)]# push tftp "download image 192.0.2.151 summitX-12.4.5.3.xos secondary \rn\r" summitX-12.4.5.3.xos os candidate
Push os/candidate ...
TFTP server at 192.0.2.151:69
Executing: download image 192.0.2.151 summitX-12.4.5.3.xos secondary \rn\r
Transfered summitX-12.4.5.3.xos
```

## SFTP Example

This SFTP example demonstrates pushing a stored firewall configuration to a Linux system:

```
[admin@UplogixLM (port1/5)]# push sftp â€“dedicated "scp ${user}@${ip}:${path} /etc/sysconfig/iptables" startup-config iptables
Push startupConfig/custom ...
SFTP/SCP service at 169.254.100.14:22
Executing: scp ${user}@${ip}:${path} /etc/sysconfig/iptables
Responding to password prompt
SFTP/SCP started
SFTP/SCP done
Transfer complete
```

# ASCII Escape Sequences

Control characters and special characters that might be necessary as part of a command (or chain of commands) on a managed device can be embedded in the command string the driver executes on the managed device.  Any command that requires double quotes must be escaped, as the Uplogix CLI uses double quotes to enclose the command that is to be issued on the managed device.  Here are a few useful escape sequences:

|Sequence/Characters|	Meaning|
|:--|:--|
|\xhh|	ASCII character with hexadecimal value 0xhh|
|\cX	|Control character corresponding to X|
|\r|	Carriage return|
|\n	|New line|
|\t|	Tab character|
|\\\	|Backslash character|