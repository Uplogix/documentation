<!-- 5.4 -->

Provides direct access to the console port of the device. The default preference is to snapshot the operational (running) configuration for transactional rollback.

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
terminal
```

# Subcommands 

While using the terminal pass-through application, the following commands are available to provide additional functionality:

* **~a** Authentication Wizard

* **~b** Send break signal

* **~c** Incremental Commit

* **~e** Turn on local echo

* **~f** Start or Stop the FTP server

* **~g** Enable/disable SFTP/SCP service

* **~h** Show this help menu

* **~l** Lock port

* **~n** Append newlines to carriage returns

* **~p** Power on/off/cycle this device

* **~q** Send Solaris alternate break signal

* **~r** Rollback wizard

* **~s** Serial connection settings wizard

* **~t** Tftp server wizard

* **~x** XModem Wizard

* **~y** YModem Wizard

* **~**  Exit Terminal

Availability of commands is determined by the userâ€™s authorization.

## New for 5.4

Prior to 5.4, the **terminal** command made use of the **use system auth** privilege to automatically log users into the managed device (if the port was configured with an advanced driver and the authentication credentials stored). As a result, when users ran **terminal**, they were presented with the privileged-mode CLI of the managed device.

In 5.4, the **use system auth** privilege has been denied by default. Now, when running the **terminal** command, the Local Manager will log out of the managed device before handing control of the CLI to the user.

> Pre-existing roles, groups, and users are not affected by this change. The appropriate permission was automatically re-added during the upgrade to 5.4.

# Usage 

To start a terminal session with a device, navigate to the appropriate port and issue the **terminal** command. You may be prompted to log into the device. Terminal commands available are role-based and port-specific.

If the terminal is in use, the system returns the message:

```
Terminal pass-through is in use. Press 'x' to exit, 'f' to force break 
```
The terminal pass-through feature blocks all automated Uplogix Local Manager processes while active. It times out in five minutes to allow automated processes to continue.

The transactional configuration rollback automatically generates a rollback document that is applied within 90 seconds after the commit option is ignored. During the countdown to rollback, the system sends the ASCII bell character each time it refreshes the countdown display, to provide an audible cue that rollback is about to start.

Scheduled jobs that are already executing will complete before pass-through starts, signaled by:

```
Process is executing. Please wait or press 'x' to exit. 
```

To exit pass-through mode, press the tilde character **~** and the enter key.

When you end your session, you will be prompted to enter a comment describing the reason for your changes if changes are detected.

```
[admin@UplogixLM (port1/1)]# terminal
Press ~[ENTER] to exit
Connecting ...
Process is executing. Please wait or press 'x' to exit.
Retrieving running-config from device ...
Complete. running-config pulled.
Console session started.
DMZ-2948#
DMZ-2948#
You have been idle for 150 seconds. Your session will end in another 150 seconds.
You have been idle for 300 seconds, your session is ending.
Disconnecting ...
Retrieving running-config from device ...
Complete. running-config pulled.
```

# In the Uplogix web interface

**Inventory > Local Manager page > port detail > Terminal button**

# History 

1.06 - FTP server added.
3.2 - Lock capability and comment prompt on exit added.
3.3 - Local echo and CR+NL added.

# Related commands 
--
