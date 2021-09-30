<!-- 5.4 -->
The purpose of this document is to detail the installation and configuration of an Uplogix Local Manager (LM) to manage and facilitate remote connectivity to a Palo Alto firewall.

# Features
Supports Palo Alto firewalls running PAN-OS version 4 or higher.

# Physical Connection

Connect a free serial port on the Local Manager to the Palo Alto's RS-232 console management port with a standard Cat-5 cable.

# Recommended Configuration

For proactive monitoring of the Palo Alto's status, and to ensure the availability of backup configurations, it is recommended that:
- The Local Manager serial port connected to the Palo Alto is configured via the **config init** command.
- Automatic backup of the configuration is scheduled.
- Tthe paloAltoStatus ruleset is scheduled 

# Configuring the Port

To configure the Local Manager for connection to a Palo Alto firewall, navigate to the port that the Palo Alto is connected to, run the command config init, and follow the prompts as below (substituting your Palo Alto's IP address):

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

To save the Palo Alto's configuration to the LM, navigate to the port that the Palo Alto is connected to and run the either of the following commands, substituting the LM's IP address:

```
pull sftp -file running-config.xml "scp export configuration from running-config.xml to ${user}@${ip}:${path}" running-config current

pull tftp "tftp export configuration to 10.0.1.2 from running-config.xml" running-config.xml running-config current 

Example: 

[admin@UplogixLM]# port 1/4

Palo Alto firewall

[admin@UplogixLM (port1/4)]# pull tftp "tftp export configuration to 10.0.1.2 from running-config.xml" running-config.xml running-config current
```

##Automatic Configuration Backup

To configure the Local Manager to back up the running-config of a Palo Alto firewall every three hours, use one of the following commands:
```
config schedule pullSftp -file running-config.xml "scp export configuration from running-config.xml to ${user}@${ip}:${path}" running-config current -d 10800

config schedule pullTftp "tftp export configuration to 10.0.1.2 from running-config.xml" running-config.xml running-config current -d 10800
```

##Restore Configuration

There are multiple steps to restore a backup configuration to a Palo Alto firewall. The file may be transferred via SCP or TFTP. 

First, navigate to the port the Palo Alto is connected to and stage the file to be restored as a *candidate* configuration:

```
[admin@UplogixLM (port1/4)]# copy running-config previous candidate
```

Next, run one of the following commands, substituting the LM's IP address for 10.0.1.2:

```
push sftp -file running-config.xml "scp import configuration ${user}@${ip}:${path} \r configure \r load config from running-config.xml \r commit \r exit" running-config candidate

push tftp "tftp import configuration 10.0.1.2/running-config.xml \r configure \r load config from running-config.xml \r commit \r exit" running-config.xml running-config candidate
```

Upon entering one of those commands, the Uplogix LM will connect to the Palo Alto's CLI, transfer the candidate configuration, and apply the configuration.

#Monitoring Palo Alto Status

##Palo Alto Health Check Ruleset

The Local Manager can be configured to monitor the status of a managed Palo Alto using the paloAltoStatus rule set. The LM will check the Palo Alto for environmental alarms and high CPU usage. High CPU usage or system heat will trigger an alarm on the LM. 

To load the paloAltoStatus rule set on the LM, copy and paste the following into the LM at the system level:

```
config rule no paloAltoChassisPoll
config rule paloAltoChassisPoll
description - ruleset to query Palo Alto for CPU info, environmental alarms, etc.
conditions
console.dsr equals true AND
console.cts equals true
exit
action clearValue monitor cpuUse
action clearValue monitor envAlarm
action execute -setValue monitor envAlarm $1 -pattern "(True)" -command "show system environmentals thermal \r " -raw
action execute -setValue monitor cpuUse $1 -pattern "(\d?\d)\.\d%us" -command "show system resources \r q "  -raw
exit
 
config rule no paloAltoEnvironmentalAlarm
config rule paloAltoEnvironmentalAlarm
description - sends an alarm when "show system environmentals" returns "true" for an alarm state
conditions
compare-value monitor envAlarm = True
exit
action alarm GENERIC -a "system hot"
action writeStatus hot
exit
 
config rule no paloAltoCPUAlarm
config rule paloAltoCPUAlarm
description
conditions
compare-value monitor cpuUse >= 80
exit
action alarm CPU_LOAD_MAJOR -a "CPU load high"
action writeStatus CPU high
exit
 
config rule no paloAltoNoResponse
config rule paloAltoNoResponse
description - when the response to the CPU check has been null for three minutes, report an inability to get a resposne
conditions
NOT has-value monitor cpuUse AND
NOT has-value monitor envAlarm
exit
action alarm GENERIC -a "device not responding to CPU and environmental checks"
action writeStatus no response
exit
 
config rule no paloAltoSerialDisconnected
config rule paloAltoSerialDisconnected
description
conditions
NOT console.dsr equals true AND
NOT console.cts equals true
exit
action alarm GENERIC -a "serial cable unplugged or device powered down"
action writeStatus no connection
exit
 
 
 
config ruleset paloAltoStatus
rules
paloAltoChassisPoll | paloAltoSerialDisconnected | paloAltoNoResponse | paloAltoCPUAlarm | paloAltoEnvironmentalAlarm
exit
exit
```

To configure the LM to use the paloAltoStatus rule set to monitor a Palo Alto firewall, navigate to the port that the Palo Alto is connected to and run the following command:

```
config monitor chassis paloAltoStatus
```

#Connecting to the Web Interface

##Port Forwarding

The Local Manager can facilitate connections to the Palo Alto's web interface using the port forwarding feature. Run configure protocol forward on the port the Palo Alto is connected to and add an entry as below: 

```
[admin@UplogixLM (port1/4)]# config protocol forward
[forward]# management 443 https
[forward]# exit
```

Users may now connect to the web interface through an SSH tunnel using the port forwarding feature. In SSh applet on the Control Center, click *Terminal*, then *Forward*. Select the Palo Alto's port, enter 443 for the port number, and click *Apply*. Now, port 443 on 127.0.0.1 on your workstation will connect through the SSH tunnel created by the LM to the web interface on the Palo Alto.

![](http://www.uplogix.com/support/docs/img/PaloAlto/PortForwarding.png)