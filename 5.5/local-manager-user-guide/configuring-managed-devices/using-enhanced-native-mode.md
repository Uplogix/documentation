<!-- 5.4 -->

# Overview

Enhanced native mode allows the Local Manager to automate basic commands for devices for which no advanced driver exists. Using regular expressions, the Local Manager can log in, log out, and recognize the command prompt. Coupled with rules, monitors and the ability to pull and push files using SFTP/SCP/TFTP, the enhanced native driver provides a very significant amount of automated functionality to bridge the gap between native mode and an advanced driver. Enhanced native mode allows users to configure a port such that it will:

- Automatically authenticate with the device when the user runs the terminal command.
- Automatically exit the device command line when exiting a terminal session, when the idle timeout is reached, or if the userâ€™s session is lost unexpectedly.
- Schedule monitors with custom rules for device monitoring/testing.

Enhanced native settings become available after running **config init** and selecting enhanced as the device make. Enhanced-specific options are:
â€ƒ

|Option	|Default Value	|Description|
|:----|:----|:----|
|command prompt|	[#>]|	A regular expression representing the command prompt of the managed device. By default, matches all command prompts that end in # or >.|
|login prompt|	sername:\s	|A regular expression representing the username prompt. For example, the default value of sername: followed by a whitespace (\s) would match all the prompts "Username:", "Username:", and "Enter Username:"|
|password prompt	|ssword:\s|	A regular expression representing the password prompt. For example, the default value of ssword: followed by whitespace (\s) would match all the prompts "Password:", "Password:", and "Enter Password:"|
|logout command	|exit|	The command used to exit the managed deviceâ€™s command line interface. Other examples include logout or quit.|
|wakeup command|	\r|	The command used to wake up the managed device. In other words, cause the device to present a login prompt when the default line feed will not result in a prompt. For example, if the user must enter CTRL+C key sequence to get a login prompt, then the wakeup command should be \c.|

The default values will not work with all devices. Before running **config init**, terminal into your device (in native mode or with a workstation) and take note of the various command prompts as well as the login/password prompt. 

> Some trial and error may be necessary before finding the most robust prompt definition for your device.

# Regular Expressions

Regular expressions are used to specify the command, username, and password prompts for the managed device. Please contact Uplogix Support for assistance creating regular expressions for your specific device. Below are basic operations:

|Characters|Description|
|:-|:-|
|[ ]| 	Brackets: Matches any of the characters within the brackets.  <br>Example 1:  [#>!] matches a prompt that ends with #, >, or !  <br>Example 2:  [~!]# matches a prompt that ends with ~# or !#||
|\|| 	Pipe: Separates alternative strings.<br>Example:  router>\|router# matches a prompt ending in router> or router#|
|() |	Parentheses: Provides order of operation when evaluating expressions.<br>Example:  router(>\|#) matches router first, then either > or # at the end of it. Without the parenthesis, router>\|# would match router> and #.|
|\* | 	Asterisk: Describes a possibility for zero or more instances of the character preceding it.<br>Example:  pas*word matches paword (zero instances of s), pasword (1 instance), password and passsword (multiple instances).|
|\s	|Represents any form of whitespace, including tab, newline, space, carriage return, form-feed, etc.|

# Examples

|Device Configuration|	Local Manager Configuration|
|:-|:-|
|command prompts:<br>hostname>|command prompt: >|
|login prompts:<br>login:|	login prompt: ogin:\s|
|password prompts:<br>password:|	password prompt: ssword:\s|
|logout command:<br>exit|	logout command: exit|
|command prompts:<br>hostname><br>hostname#<br>hostname!|	command prompt: [>#!]|
|login prompts<br>Username:|	login prompt: sername:\s|
|password prompts:<br>User Secret:|	password prompt: ecret:\s|
|logout command:<br>quit|	logout command: quit|
|command prompts:<br>user name\$<br>group name!<br>group name\=<br>group name!=<br>|	command prompt: [$!=]\s|
|login prompts<br>User Email:<br>Group Email:<br>User Number<br>Group Number|login prompt: (mail&#124;umber):\s|
|password prompts:<br>User Password:<br>Group password:|password prompt: ssword:\s|
|logout command:<Br>close|logout command: close|

# Configuring a Port in Enhanced Native Mode

To configure a port for enhanced native mode, follow these steps. Log in to the Local Manager via SSH or the console management port. Navigate to the port using the **port [slot]/[number]** command and **run config init**. When prompted for make, enter enhanced.

```
[admin@UplogixLM (port1/2)]# config init
--- Enter New Values ---
description: Extreme 150
make [native]: enhanced
model: 
os: 
os version: 
management IP: 192.0.2.111
command prompt [[#>]]: 
login prompt [sername:\s]: login:\s
password prompt [ssword:\s]: 
logout command [exit\r]: 
wakeup command [\r]: 
console username: admin
console password: 
Serial Bit Rate [9600]: 
Serial Data Bit [8]: 
Serial Parity [none]: 
Serial Stop Bit [1]: 
Serial Flow Control [none]: 
Do you want to commit these changes? (y/n): y
```

# Timeout Configuration

By default, the enhanced native driver waits up to 5 seconds for the managed device to respond (i.e. to present login and password prompts as well as the CLI prompt after issuing a command).  Some devices may not respond to the driver quick enough, causing the driver to fail to login or detect the state of the managed device.  A port property named **Enhanced_TimeoutSecond**s can be specified with a timeout value (in seconds) to override the default value â€“ the timeout value can be extended or shortened using this mechanism.  For example, to configure this value to 8 seconds, login to the Local Manager, navigate to the enhanced native port, and issue the **config properties** command as follows:

```
[admin@UplogixLM]# port 1/1
enhanced   
[admin@UplogixLM (port1/1)]# config properties
[config properties]# Enhanced_TimeoutSeconds 8
[config properties]# exit
```

To view enhanced native property settings, issue the **show properties** command at the Local Manager port:

```
[admin@xyzcoAuz (port1/1)]# show properties
Enhanced_CommandPrompt: [#>]
Enhanced_LoginPrompt: login:\s
Enhanced_LogoutCommand: exit\r
Enhanced_PasswordPrompt: ssword:\s
Enhanced_TimeoutSeconds: 8
Enhanced_WakeupCommand: \r
```

# Configuration and OS File Backup and Restoration

If the managed device supports SFTP, SCP or TFTP and supports commands to back up its configuration and OS files to a SFTP/SCP/TFTP server, our Pull/Push SFTP and TFTP command functionality can be used to create automatic file backups for example.