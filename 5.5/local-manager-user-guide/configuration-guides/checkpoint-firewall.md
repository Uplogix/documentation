<!-- 5.4 -->

The purpose of this document is to detail the installation and configuration of an Uplogix Local Managers (LM) to manage and facilitate remote connectivity to a Checkpoint firewall.

# Features

* Supports Checkpoint firewalls running version R75.4 with Uplogix 500 or 5000

# Physical Connection

Connect a free serial port on the Uplogix to the Checkpointâ€™s RS-232 console management port with a standard Cat-5 cable.

# Configuring the Port

To configure the Uplogix LM for connection to a Checkpoint firewall, navigate to the port that the Checkpoint is connected to, run the command **config init**, and follow the prompts as below (substituting your Checkpointâ€™s IP address for 203.0.113.16):

```
[admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: Checkpoint firewall
make [native]: enhanced
management IP: 203.0.113.16
Configure dedicated ethernet port? (y/n) [n]:
command prompt [[#>]]:
login prompt [(ogin:\s]: [(?<!Last\s)login:\s
password prompt [assword:\s]: Password:\s
logout command [exit\r]:
wakeup command [\r]:
console username []: admin
console password []: ********
confirm password []: ********
Serial Bit Rate [9600]:
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
Scheduling default jobs
Testing job rulesMonitor
Job rulesMonitor was successful
Job rulesMonitor was scheduled
```

The default console settings for the Checkpoint firewall are 9600 bit rate, 8 serial data bit, no serial parity, serial stop bit 1, no flow control.

# Managing Configurations

## Backup Configuration 

The Uplogix Local Manager can save up to twenty backup images on the LMâ€™s filesystem for use in restoring a configuration or pushing a configuration to a new Checkpoint.

To save the Checkpointâ€™s configuration to the LM, navigate to the port that the Checkpoint is connected to, use the terminal command to connect to the console port of the Checkpoint, start the TFTP server with the command ~t, and then run the backup command on the checkpoint as in the example below (substituting the LMâ€™s IP address for 64.129.60.134). Once the backup has been transferred to the LM, use ~t and press 3 to save the uploaded backup. Verify the backup was saved to the LMâ€™s file system with the command **show directory**.

```
[admin@UplogixLM]# port 2/7
enhanced  CLISH
Checkpoint GAIA

[admin@UplogixLM (port2/7)]# terminal

Press ~[ENTER] to exit.

Connecting ...

login: admin
Password:
Last login: Mon Mar 24 14:49:11 on ttyS0

gw-50ed44>

~t
Start the TFTP server? (y/n) [y]: y
TFTP server started.
The TFTP server is currently running on /64.129.60.134:69.
No files are currently available for download

No files have been uploaded

1) Add file to download list
2) Remove file from download list
3) Save uploaded file
4) Stop TFTP server
5) Return
Please select an option: 5

gw-50ed44> add backup tftp ip 64.129.60.134
Creating backup package. Use the command 'show backups' to monitor creation progress.
After backup is finished, please verify it was sucessfully transfered to the remote machine.
gw-50ed44> show backups
Backup package is under creation now.
gw-50ed44>
show backups
gw-50ed44>
gw-50ed44>

~t
The TFTP server is currently running on /64.129.60.134:69.
No files are currently available for download

Uploaded files:
backup_gw-50ed44_24_3_2014_15_13.tgz

1) Add file to download list
2) Remove file from download list
3) Save uploaded file
4) Stop TFTP server
5) Return
Please select an option: 3
Uploaded files:
1) backup_gw-50ed44_24_3_2014_15_13.tgz
2) Cancel
Please select an option: 1
Save 'backup_gw-50ed44_24_3_2014_15_13.tgz'? (y/n) [y]: y
1) OS Image
2) Running Configuration
3) Startup Configuration
4) Cancel
Please select an option: 2
'backup_gw-50ed44_24_3_2014_15_13.tgz' was saved successfully.


1) Add file to download list
2) Remove file from download list
3) Save uploaded file
4) Stop TFTP server
5) Return
Please select an option: 5

gw-50ed44>

~<ENTER>
Console session ended.


Disconnecting ...

Logging out of device...

[admin@UplogixLM (port2/7)]# show dir
Type     Version    Name
-------  ---------  ------------
Config
Running*
current    backup_gw-50ed44_24_3_2014_15_13.tgz
previous   backup_gw-430c6e_11_Mar_2014_15_12.tgz

OS
current    backup_gw-50ed44_19_3_2014_14_51.tgz
previous   backup_gw-50ed44_19_3_2014_13_16.tgz

* additional archived versions are available. Execute show dir â€“v
```

## Restore Configuration

To restore a backup image to a Checkpoint firewall, navigate to the port the Checkpoint is connected to, use the **terminal** command to connect to the Checkpointâ€™s CLI, and use ~t to stage the file to be used. Then run the set backup restore command on the Checkpoint, substituting the IP address of the LM being used for 64.129.60.134. Check the restore status with show backups, and when the Checkpoint is finished restoring restart with reboot.

```
[admin@UplogixLM]# port 2/7
enhanced  CLISH
Checkpoint GAIA

[admin@UplogixLM (port2/7)]# terminal

Press ~[ENTER] to exit.


Connecting ...



Console session started.  Press ~[ENTER] to exit.

gw-50ed44>

~t

The TFTP server is currently running on /64.129.60.134:69.

1) Add file to download list
2) Remove file from download list
3) Save uploaded file
4) Stop TFTP server
5) Return
Please select an option: 1
1) OS Image
2) Running Configuration
3) Startup Configuration
4) Cancel
Please select an option: 2
1) Current
2) Previous
3) Done
Please select an option: 1
backup_gw-50ed44_24_3_2014_15_13.tgz has been made available for download.

1) Add file to download list
2) Remove file from download list
3) Save uploaded file
4) Stop TFTP server
5) Return
Please select an option: 5

gw-50ed44>
This system is for authorized use only.
login: admin
Password:
Login incorrect

login: admin
Password:
Last login: Mon Mar 24 15:12:26 on ttyS0

gw-50ed44> set backup restore tftp ip 64.129.60.134 file backup_gw-430c6e_11_Mar__2014_15_12.tgz
gw-50ed44> show backups
Restoring from backup package backup_gw-430c6e_11_Mar_2014_15_12.tgz.
Don't forget to reboot the machine after it's finished.
gw-50ed44> reboot
Are you sure you want to reboot?(Y/N)[N]
y
```

# Connecting to the Web Interface

## Port Forwarding

The Uplogix Local Manager can facilitate connections to the Checkpointâ€™s web interface using the port forwarding feature. Run configure protocol forward on the port the Checkpoint is connected to and add an entry as below: 

```
[admin@UplogixLM (port2/7)]# config protocol forward
[forward]# management 443 https
[forward]# exit
```

Users may now connect to the web interface through a SSH tunnel using the port forwarding feature. In the Uplogix CLI applet, click Terminal, then Forward. Select the Checkpointâ€™s port, enter 443 for the port number, and click Apply. Now, port 443 on 127.0.0.1 on your workstation will connect through the SSH tunnel created by the LM to the web interface on the Checkpoint.