# Overview
The Local Manager's Command Line Interface (CLI) allows you to configure and manage all aspects of the appliance and the devices it manages. All hardware platforms run the same version of software and use the same CLI.

The CLI is accessible from the onboard console port or via the network using SSH. Terminal access (TTY) is available via dial-in modem and Telnet, but both are disabled by default for security reasons.

# Structure of the CLI

The command line employs a hierarchy for organizing the Local Manager, ports, power controllers, and modems. **These are called resources**. The system resource is the root resource.
 
To return to the system resource from another resource, use the **exit** command.

| Resource | Description | Command |
| - | - |
| system | The root resource. All Local Manager configuration and user management functions are accessed from this resource. | exit (return from another resource) |
| port | Use to configure and manage a device connected to a device port on the Local Manager. | port slot/number (from any resource) |
| <del>powercontrol</del> | <del>Use to configure and manage an external power controller and map its outlets to devices managed by the Local Manager.</del> | <del>powercontrol (from the system resource)</del> |
| modem	| Use to configure embedded and external modems and related settings. | modem (from the system resource) |
 
> **LMS v5.4 and later** - The reserved ***powercontrol*** keyword and related resource have been removed. Any port on the Local Manager can now be used as a power controller.
 
# Opening and closing a CLI session
To open a CLI session from a workstation connected to the management console port, open a terminal session using one of the supported terminal clients:

* Windows HyperTerminal
* ZTerm (Macintosh OS X)
* Minicom (Unix/Linux)
* PuTTy

The default console connection settings are 9600 baud, 8 data bits, 1 stop bit, no parity, and no flow control. For best results, set the terminal emulator to use ANSI encoding.

To open a CLI session over the network using SSH, open a Secure Shell (v2) connection using one of the supported Secure Shell clients:

* Control Center SSH Applet
* PuTTY
* SSHÂ® Tectiaâ„¢
* VanDykeÂ® SecureCRTÂ®
* SSHTerm for Windows
* iTerm for Macintosh OS X
* UNIXâ€™s built-in ssh command

For example, in a UNIX command line, type **ssh admin@198.51.100.254**

Substitute the IP address of the Local Manager.

## Logging in

After connecting to the Local Manager, you will be prompted for a username and password. The default username is **admin** and the default password is **password**.

> Usernames and passwords are case-sensitive.

## Closing the session
To end your CLI session with the Local Manager, issue the **logout** command.

# Command types

Many commands are executed without dialog. Some, such as **ping**, require command arguments; others, like **logout** and **shutdown**, do not take command arguments.

Interactive commands prompt for new information and may display current settings. For example:

```
[admin@UplogixLM]# config date
Displayed time is 12/30/2020 10:33:16 CST
System time is    12/30/2020 16:33:16 UTC
Change these? (y/n) [n]: y
Current system time (MM/dd/yyyy HH:mm:ss):12/30/2020 16:36:00
Displayed time is 12/30/2020 10:36:02 CST
System time is    12/30/2020 16:36:02 UTC 
```

In this example, the current date and time is displayed (both UTC and local time zone). A prompt asks whether you wish to change the settings. If you answer **y**, the Local Manager prompts for the new date and time. After entering this information, the Local Manager displays the new date and time and returns to the system prompt.

Some interactive commands present default or current settings, which can be accepted by pressing the Enter key.

Some commands open editors in which you can issue subcommands in any order. To save changes and return to the main command line from an editor, use the **exit** command.

# Command shortcuts

The command line provides several ways to reduce the amount of typing required in the command line.

## Repeating commands

Repeat the most recent commandâ€”and go back to earlier commands in reverse sequenceâ€”by pressing the up arrow key and then the Enter key. 

## Abbreviating commands

As with many command line interfaces, the Uplogix command line allows you to abbreviate commands to the shortest string that uniquely identifies the command.

For example, shorten the **ping** command to **pi**. Similarly, shorten **show dashboard** to **sh das**.

An error results if the **ping** command is shortened to **p**. This is because **p** matches all other commands beginning with the letter p. Similarly, an error results if **show dashboard** is shortened to **sh da** because this string matches **show date**.

The exception is **shutdown**. To minimize the potential for accidental shutdown, this command is not accepted if it is abbreviated.

## Using wildcard characters

The command line allows the \* character as a wildcard. For example, issue the command **show rule cpu\*** to view all rules that have names starting with cpu.

## Paging through command feedback

Some commands return large amounts of information. When reviewing long displays of command feedback, type **<** to return to the beginning of the display or **>** to go to the end.

## Canceling out of interactive commands

Use **CTRL-C** to exit interactive commands without saving changes.

# Looping commands

If you find yourself running the same command repeatedly, you can use the **loop** command to automate the process.

The syntax is:

```
loop<seconds>: <command to execute>
```

For example, to run the **show alarm** command every 30 seconds:

```
[admin@UplogixLM]# loop30: show alarm
Looping with delay 30s
GMT       Elapsed     Device     Context     Message                                                                   
-----     -------     ------     -------     --------------------------------------------------------------------------
11/30     0:23                                System and management server clocks are more than 20 seconds out of sync.
```

# Redirecting command output to a file

Some **show** commands return more information than is practical to view in the command line window. For example, the **show role** command may produce several screens of output and the **show buffer** command will typically produce several hundred screens. In these cases it may be preferable to copy the output to a file that can be examined later.

Use the pipe character | to redirect the output of a command via FTP or SCP. The syntax is: 

```
<command> | <ftp | scp | mailto username@host:path/to/file
```

For example, to use SCP to redirect the output of the **show config** command to another computer:

```
show config | scp username@host:path/to/file
```

where username@host:path/to/file specifies the destination for the data.

Need help using the pipe redirect? Enter **| ?** in the command line.

# Redirecting command output to email

Some **show** commands return more information than is practical to view in the command line window. For example, the **show role** command may produce several screens of output and the **show buffer** command will typically produce several hundred screens. In these cases it may be preferable to copy the output to an email that can be examined later. 

This functionality requires the Local Manager Email server settings to be properly configured (**config system email** command).

Use the pipe character | to redirect the output of a command as a file attachment in an email to the specified email address. The syntax is: 

```
<command> | mailto username@host:<filename>
```

For example, to use SCP to redirect the output of the show config command to another computer:

```
show config | scp username@host:path/to/file
```

where username@host:path/to/file specifies the destination for the data.

Need help using the pipe redirect? Enter **| ?** in the command line.

For example, to send the contents of a port buffer to the support@uplogix.com email address as a file named â€œbuffer.logâ€, use the following syntax:

```
[admin@UplogixLM] (port1/1)# show buffer | mailto support@uplogix.com:buffer.log
```

# Parsing Output

Using the pipe character, you can redirect the output of a command to grep for parsing. The syntax is:
```
<command> | grep â€œkeywordsâ€
```
For example, you can parse the output of **show user \*** to pull out email addresses:
```
[admin@UplogixLM]# show user * | grep email
email support@uplogix.com
email tjones@uplogix.com
```

# Viewing context-sensitive help

To show command usage notes, type the command and then ?.
```
[admin@UplogixLM]# port ?
usage: port <slot number>/<port number>

[admin@UplogixLM]# config export ?
usage: export <method> <target>
              methods: ftp, scp, usb

Export via FTP
ex. config export ftp <userId@host:fileName>
Export via SCP
ex. config export scp <userId@host:fileName>
Export via USB
ex. config export usb <fileName>
```
To view a list of available commands from any resource within the command line, type **?**. The commands listed will be limited to the allowed actions for your role in the current resource.

For example, if you navigate to the modem resource and type **?** on a line by itself, the Local Manager returns the following help text:
```
[admin@UplogixLM (modem)]# ?
Uplogix LMS v6.0 35585

config                   Edit settings
copy                     Copy file to another port or from an external location
exit                     Exit modem menu
history                  Display command history
logout                   Logout
outband                  Interact with outband
port                     Commands specific to port
power                    Control power of external modem on console
ppp                      Interact with PPP
pull                     Pull files from modem
show                     Display settings and status
suspend                  Suspend automated or recovery processes
terminal                 Terminal access
```

Usage notes allow you to drill down into a command:

```
[admin@UplogixLM]# show ?
Uplogix LMS v6.0 35585

alarms                   Display current alarms
all                      Display all device configuration
capture                  Display captured packets
config                   Display system configuration
dashboard                Display summary of the system and its managed devices
date                     Display system time
directory                Display overall file system info
environment              Display current temperature and humidity
events                   Display events
group                    Display group settings
install-history          Display update history
log                      Display logs
monitors                 Display list of current monitors
outband                  Display outband status
ports                    Display summary of port configurations
privileges               Display privileges for users
restrict                 Display restrict details
role                     Display security role information
rule                     Display rule details
ruleset                  Display ruleset details
schedules                Display currently scheduled processes
session                  Display single session by id
sessions                 Display session data [by user]
system                   Display system settings
user                     Display user data
version                  Display hardware and software version information
who                      Display information of currently logged-in users


[admin@UplogixLM (modem)]# show alarms ?
usage: alarms [options]

--- options ---

  -all        Current and cleared alarms
  -cleared    Cleared alarms
  -n <count>  Maximum number of alarms
  -v          Use multiple lines
```

# Viewing the command history

The **history** command displays up to the last 20 commands (if available) from the current resource.

```
[admin@UplogixLM]# history
1. modem
2. config init
3. show ?
4. show alarms
5. history
```

To execute a listed command, enter ! followed by the command number.

```
[admin@UplogixLM]# !4
show alarms
There are no alarms right now.
```

# Setting CLI page length

By default, the Local Manager automatically tries to determine the appropriate number of lines to display in the CLI window before providing a scroll prompt. If the appropriate page length cannot be determined, the CLI displays 24 lines before presenting a scroll prompt.

To change the number of lines displayed, use the **config system page-length** command:

```
[admin@UplogixLM]# config system page-length
Page length preference is auto.
Change this? (y/n) [n]: y
Page length preference (2 or more lines or auto):50
```

In this example, the command line will display 50 lines before prompting you to press a key to scroll the display.