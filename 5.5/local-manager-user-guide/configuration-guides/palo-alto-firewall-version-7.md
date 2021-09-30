<!-- 5.4 -->
The purpose of this document is to detail the installation and configuration of an Uplogix Local Manager (LM) to manage and facilitate remote connectivity to a Palo Alto firewall.

#Features
Supports Palo Alto firewalls running PAN-OS version 7 or higher.

#Physical Connection

Connect a free serial port on the Local Manager to the Palo Alto's RS-232 console management port with a standard Cat-5 cable.

#Recommended Configuration

For proactive monitoring of the Palo Alto's status, and to ensure the availability of backup configurations, it is recommended that:
- The Local Manager serial port connected to the Palo Alto is configured via the **config init** command
- Automatic backup of the configuration is scheduled 
- The paloAltoStatus ruleset is scheduled

#Configuring the Port

To configure the Local Manager for connection to a Palo Alto firewall, navigate to the port that the Palo Alto is connected to, run the command **config init**, and follow the prompts as below (substituting your Palo Alto's IP address):

```
[admin@UplogixLM (port1/4)]# config init
--- Enter New Values ---
description: Palo Alto firewall
make [native]: enhanced
management IP: 203.0.113.16
Configure dedicated ethernet port? (y/n) [n]:
command prompt [[#>]]:
login prompt [(ogin:\s]: (?<!(?:ast|uccessful)\s)[lL]ogin:\s
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

The default console settings for the Palo Alto firewall are 9600 bit rate, 8 serial data bit, no serial parity, serial stop bit 1, and no flow control.

#Managing Configurations

##Back up Configuration 

The Uplogix Local Manager can save up to twenty backup images on its file system for use in restoring a configuration or pushing a configuration to a new Palo Alto. The file can be transferred to the LM via TFTP or SCP.

To save the Palo Alto's configuration to the LM, navigate to the port that the Palo Alto is connected to and run the either of the following commands, substituting the LM's IP address.

```
pull sftp -file running-config.xml "scp export configuration from running-config.xml to ${user}@${ip}:${path}" running-config current

pull tftp "tftp export configuration to 10.0.1.2 from running-config.xml" running-config.xml running-config current 
```

Example: 

```
[admin@UplogixLM]# port 1/4

Palo Alto firewall

[admin@UplogixLM (port1/4)]# pull tftp "tftp export configuration to 10.0.1.2 from running-config.xml" running-config.xml running-config current
```

##Automatic Configuration Backup

To configure the Local Manager to back up the running-config of a Palo Alto firewall every three hours, use one of the following commands:
```
config schedule pullSftp "scp export configuration from running-config.xml to ${user}@${ip}:${path}" running-config current -d 10800

config schedule pullTftp "tftp export configuration to 10.0.1.2 from running-config.xml" running-config.xml running-config current -d 10800
```

##Restore Configuration

There are multiple steps to restore a backup configuration to a Palo Alto firewall. The file may be transferred via SCP or TFTP. 

First, navigate to the port the Palo Alto is connected to and stage the file to be restored as a *candidate* configuration:

```
[admin@UplogixLM (port1/4)]# copy running-config previous candidate
```

Next, run one of the following commands, substituting the LM's IP address.

```
push sftp -file running-config.xml "scp import configuration ${user}@${ip}:${path} \r configure \r load config from running-config.xml \r commit \r exit" running-config candidate

push tftp "tftp import configuration 10.0.1.2/running-config.xml \r configure \r load config from running-config.xml \r commit \r exit" running-config.xml running-config candidate
```

Upon entering one of those commands, the LM will connect to the Palo Alto's CLI, transfer the candidate configuration, and apply the configuration.

#Monitoring Palo Alto Status

##Palo Alto Health Check Ruleset

The Local Manager can be configured to monitor the status of a managed Palo Alto using the PaloAltoChassisRules rule set. The LM will check the Palo Alto for environmental alarms and high CPU usage. High CPU usage or system heat will trigger an alarm on the LM. 

To load the PaloAltoChassisRules rule set on the LM, copy and paste the following into the LM at the system level:

```
config rule no PaloAltoCPUCheck0
config rule PaloAltoCPUCheck0
action execute -pattern "(\d?\d\.\d?)%id" -command "set cli scripting-mode on\rshow system resources\r" -raw -multiline -setValue monitor CPUid
le $1
conditions
true
exit
exit

config rule no PaloAltoCPUCheck1
config rule PaloAltoCPUCheck1
description a rule to send an alarm when CPU idle is below a certain number - adjust target as appropriate
action alarm GENERIC -a "CPU usage above 0%"
conditions
compare-value monitor CPUidle <= 99.9
exit
exit

config rule no PaloAltoMemoryCheck0
config rule PaloAltoMemoryCheck0
action execute -pattern "(\d*)k free" -command "set cli scripting-mode on\rshow system resources\r" -raw -multiline -setValue monitor MemoryFre
e $1
conditions
true
exit
exit

config rule no PaloAltoMemoryCheck1
config rule PaloAltoMemoryCheck1
description a rule to send an alarm when free memory is below a certain number - adjust target as appropriate
action alarm GENERIC -a "free memory below 1000000"
conditions
compare-value monitor MemoryFree <= 1000000
exit
exit

config rule no PaloAltoDiskCheck0
config rule PaloAltoDiskCheck0
action execute -pattern "(\d?\d?\d)%" -command "show system disk-space" -setValue monitor disk1usage $1 -setValue monitor disk2usage $2 -setVal
ue monitor disk3usage $3 -setValue monitor disk4usage $4 -setValue monitor disk5usage $5
conditions
true
exit
exit

config rule no PaloAltoDiskCheck1
config rule PaloAltoDiskCheck1
description a rule to send an alarm when disk usage is above a certain number - adjust target percentage as appropriate
action alarm GENERIC -a "disk usage over 80%"
action writeStatus DISK USAGE HIGH
conditions
compare-value monitor disk1usage >= 80 OR
compare-value monitor disk2usage >= 80 OR
compare-value monitor disk3usage >= 80 OR
compare-value monitor disk4usage >= 80 OR
compare-value monitor disk5usage >= 80
exit
exit


config ruleset no PaloAltoChassisRules
config ruleset PaloAltoChassisRules
rules
PaloAltoCPUCheck0 | PaloAltoCPUCheck1 | PaloAltoMemoryCheck0 | PaloAltoMemoryCheck1 | PaloAltoDiskCheck0 | PaloAltoDiskCheck1
exit
exit

```

To configure the Uplogix LM to use the PaloAltoChassisRules rule set to monitor a Palo Alto firewall, navigate to the port that the Palo Alto is connected to and run the following command:

```
config monitor chassis PaloAltoChassisRules
```

#Connecting to the Web Interface

##Port Forwarding

The Local Manager can facilitate connections to the Palo Alto's web interface using the port forwarding feature. Run **configure protocol forward** on the port the Palo Alto is connected to and add an entry as below: 

```
[admin@UplogixLM (port1/4)]# config protocol forward
[forward]# management 443 https
[forward]# exit
```

Users may now connect to the web interface through an SSH tunnel using the port forwarding feature. In the SSh applet on the Control Center, click *Terminal*, then *Forward*. Select the Palo Alto's port, enter 443 for the port number, and click *Apply*. Now, port 443 on 127.0.0.1 on your workstation will connect through the SSH tunnel created by the LM to the web interface on the Palo Alto.

![](http://www.uplogix.com/support/docs/img/PaloAlto/PortForwarding.png)