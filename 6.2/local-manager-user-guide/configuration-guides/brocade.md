<!-- 5.4.2 -->

The purpose of this document is to detail the installation and configuration of an Uplogix Local Manager (LM) to manage and facilitate remote connectivity to a Brocade.

# Features

* Supports Brocade software version 07.0.01cT7e1 or higher 
* Monitors CLI availability
* Monitors CPU utilization   

# Physical Connection

Connect a free serial port on the Local Manager to the Brocade's RS-232 console management port with a standard Cat-5 cable.

# Recommended Configuration

For proactive monitoring of the Brocade's status and to ensure the availability of backup configurations it is recommended that:

* the Local Manager serial port connected to the Brocade is configured as *enhanced* via the **config init** command
* automatic backup of the configuration is scheduled 
* the below rulesets are loaded on the LM and scheduled 

# Configuring the Port

The Local Manager will use the enhanced driver to log into the Brocade and run commands. If possible, provide the enhanced driver with a username and password that will be enabled to run super user commands. Without admin privileges, the Local Manager will not be able to run the commands needed to backup configurations and perform other automation. 

If a super user account can not be provided, use the brocadeEnable rule (below) to give the Local Manager super user access so that automation can be performed.
 
To configure the Local Manager for connection to a Brocade, navigate to the port that the Brocade is connected to, run the command **config init**, and follow the prompts as below (substituting your Brocade's IP address for 203.0.113.16):

```
[admin@UplogixLM (port1/5)]# config init
--- Enter New Values ---
description [port 1/5]: Brocade
make [native]: enhanced
model:
os []:
os version:
management IP [203.0.113.16]:
command prompt [[#>]]:
login prompt [sername:\s]: (?<!Last\s)login:\s
password prompt [ssword:\s]:
logout command [exit\r]:
wakeup command [\r]:
console username: admin
console password: ********
confirm password: ********
Serial Bit Rate [9600]:
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:
Use null modem (rolled cable to device)? (y/n/auto) [y]:
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
Initialize device logging
Scheduling default jobs
Testing job rulesMonitor
Job rulesMonitor was successful
Job rulesMonitor was scheduled
```

The default console settings for the Brocade are 9600 bit rate, 8 serial data bit, no serial parity, serial stop bit 1, no flow control.

# Managing Configurations

## Backup Configuration 

The Local Manager can save a local copy of the Brocade's startup and running configurations. Up to twenty-four backup images can be saved on the LM's file system for use in restoring a configuration or pushing a configuration to a replacement Brocade. The file can be transferred to the LM via TFTP.

To manually save the Brocade's configuration to the LM, navigate to the port that the Brocade is connected to and run the one of the following commands, substituting the LM's IP address for 10.0.1.2:

```
pull tftp "copy startup-config tftp 10.0.1.2 startupConfig.txt" startupConfig.txt startup-config current

pull tftp "copy running-config tftp 10.0.1.2 runningConfig.txt" runningConfig.txt running-config current
```

Example: 


```
[admin@UplogixLM]# port 1/4

Enhanced
Brocade

[admin@UplogixLM (port1/4)]# pull tftp "copy running-config tftp 10.0.1.2 runningConfig.txt" runningConfig.txt running-config current
Pull runningConfig/current ...                                                                                                  
TFTP server at 172.30.50.135:69                                                                                                 
Executing: copy running-config tftp 10.0.1.2 runningConfig.txt                                                             
Received runningConfig.txt (576 bytes)                                                                                          
MD5: 3d045c2a788d14c879c161fdd9b061c2  
```

These files can also be saved during a terminal session by using ~t to activate the Local Manager's TFTP server and running the copy commands manually. 

## Automatic Configuration Backup

To configure the Local Manager to back up the running-config of a Brocade every three hours, use the following command:

```
config schedule pullTftp "copy running-config tftp 10.0.1.2 runningConfig.txt" runningConfig.txt running-config current -d 3600
```

To configure the Local Manager to back up the startup-config of a Brocade every day, use the following command:

```
config schedule pullTftp "copy startup-config tftp 10.0.1.2 startupConfig.txt" startupConfig.txt startup-config current -d 259200
```

## Restore Configuration

Use the following commands to restore a backup configuration to a Brocade. The file can be transferred via TFTP. 

First, navigate to the port the Brocade is connected to, and stage the file to be restored as a candidate configuration. Example: 

```
[admin@UplogixLM (port1/4)]# copy running-config previous candidate
```

Next, run the following command, substituting the LM's IP address for 10.0.1.2:

```
push tftp "copy tftp running-config 10.0.1.2 runningConfig.txt" runningConfig.txt running-config current
```

To push a stored startup-configuration to the Brocade, stage the running configuration as a candidate, and run the following command, substituting the LM's IP address for 10.0.1.2: 

```
push tftp "copy tftp startup-config 10.0.1.2 startupConfig.txt" startupConfig.txt startup-config current
```
  
These files can also be pushed during a terminal session by using ~t to activate the Local Manager's TFTP server and running the copy commands manually. 

# Allowing Brocade Automation

## Brocade Enable Rule

If a super user level account cannot be provided to the enhanced driver, automation will not work. The following rule runs the enable command and enters a password in order to allow automation. Combine the enable rule with other rules when the chassis monitor is scheduled (ie - config monitor chassis brocadeEnable | brocadeConsoleCheckRules | brocadeCpuCheckRules). 

To load the brocadeEnable rule on the Local Manager, copy and paste the following into the CLI on the system resource. Replace PASSWORD with the enable password for the Brocade.

``` 
config rule no brocadeEnable
config rule brocadeEnable 
conditions
true 
exit
action execute -command "enable\rPASSWORD\r" -timeout 3 -pattern "." -raw -setValue monitor brocadeNull $1
exit
```
	
To schedule the rule, run the command:

```
config monitor chassis brocadeEnable
```

To schedule it with other rules, combine the rules with the "|" character:

``` 
config monitor chassis brocadeEnable | brocadeConsoleCheck| brocadeCpuCheck
```

# Monitoring Brocade Status
## Brocade Console Check Ruleset

The Local Manager can be configured to monitor the status of a Brocade using the brocadeConsoleCheckRules rule set. The LM will check to see if the Brocade's command prompt is available, and send an alarm if it is not.
 
To load the brocadeConsoleCheckRules rule set on the LM, copy and paste the following into the LM at the system level:

```
config rule no brocadeConsoleCheck
config rule brocadeConsoleCheck 
conditions
true 
exit
action clearValue monitor brocadeConsoleCheckResponse
action execute -command "" -timeout 3 -pattern "(>|#)" -setValue monitor brocadeConsoleCheckResponse $1
exit


config rule no brocadeConsoleResponseOk
config rule brocadeConsoleResponseOk
conditions
compare-value monitor brocadeConsoleCheckResponse = # OR
compare-value monitor brocadeConsoleCheckResponse = #
exit
action writeStatus OK
exit


config rule no brocadeConsoleResponseNo
config rule brocadeConsoleResponseNo 
conditions
NOT compare-value monitor brocadeConsoleCheckResponse = # OR
NOT compare-value monitor brocadeConsoleCheckResponse = #
exit
action writeStatus UNKNOWN
action alarm GENERIC -a "console unresponsive"
exit


config ruleset no brocadeConsoleCheckRules
config ruleset brocadeConsoleCheckRules 
rules
brocadeConsoleCheck | brocadeConsoleResponseOk | brocadeConsoleResponseNo
exit
exit
```

To configure the Local Manager to use the brocadeConsoleCheckRules rule set to monitor a Brocade, navigate to the port that the Brocade is connected to and run the following command:

```
config monitor chassis brocadeConsoleCheckRules
```

To combine that rule set with the other rule sets, schedule them with the following command: 

```
config monitor chassis brocadeEnable | brocadeConsoleCheckRules | brocadeCpuCheckRules
```

## Brocade CPU Check Ruleset

The Local Manager can be configured to monitor the CPU utilization of a Brocade using the brocadeCpuCheckRulesrule set. The LM will check the Brocade's current CPU utilization, and send an alarm if it exceeds %80. 

The alarm threshold can be adjusted by changing the value from 80 to whatever level is desired in the line "compare-value monitor brocadeCpu1 > 80" in the brocadeCpuHigh rule, below. 

To load the brocadeCpuCheckRules rule set on the LM, copy and paste the following into the LM at the system level:

```
config rule no brocadeCpuCheck
config rule brocadeCpuCheck 
conditions
true 
exit
action execute -command "show cpu" -timeout 3 -pattern "(\d?\d?\d)\spercent busy" -multiline -setValue monitor brocadeCpu1 $1
exit


config rule no brocadeCpuHigh
config rule brocadeCpuHigh
conditions 
compare-value monitor brocadeCpu1 > 80
exit
action writeStatus CPU HIGH
action alarm GENERIC -a "CPU over %80"
action clearValue monitor brocadeCpu1
exit 


config ruleset no brocadeCpuCheckRules
config ruleset brocadeCpuCheckRules 
rules
brocadeCpuCheck | brocadeCpuHigh
exit
exit
```

To configure the Local Manager to use the brocadeCpuCheckRules rule set to monitor a Brocade, navigate to the port that the Brocade is connected to and run the following command:

```
config monitor chassis brocadeCpuCheckRules
```

To combine that rule set with the other rule sets, schedule them with the following command: 

```
config monitor chassis brocadeEnable | brocadeConsoleCheckRules | brocadeCpuCheckRules
```