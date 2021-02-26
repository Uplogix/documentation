<!-- 5.4 -->

Use the **terminal** command to communicate directly with a managed device.

# New for 5.4

Prior to 5.4, the **terminal** command made use of the **use system auth** privilege to automatically log users into the managed device (if the port was configured with an advanced driver and the authentication credentials stored). As a result, when users ran **terminal**, they were presented with the privileged-mode CLI of the managed device.

In 5.4, the **use system auth** privilege has been denied by default. Now, when running the **terminal** command, the Local Manager will log out of the managed device before handing control of the CLI to the user.

> Pre-existing roles, groups, and users are not affected by this change. The appropriate permission was automatically re-added during the upgrade to 5.4.

# Starting a terminal session

To start a terminal session with a device, navigate to the appropriate port and issue the **terminal** command. You may be prompted to log into the device. Terminal commands available are role-based and port-specific.

**Terminal commands**

Commands available in terminal sessions:

```
Uplogix terminal commands:
~a - Authentication Wizard
~b - Send break signal
~c - Incremental Commit
~e - Turn on local echo
~f - Start or Stop the FTP server
~g - Enable/disable SFTP/SCP service
~h - Show this help menu
~l - Lock port
~n - Append newlines to carriage returns
~p - Power on/off/cycle this device
~q - Send Solaris alternate break signal
~r - Rollback wizard
~s - Serial connection settings wizard
~t - Tftp server wizard
~x - XModem Wizard
~y - YModem Wizard
---
```

# Locking a terminal session

If your role on the port includes the terminal lock permission, you can issue the **~l** command to lock the terminal during long processes. Other users who try to initiate terminal sessions to the device will be notified that a terminal lock is in effect. Users with the terminal force permission on the device can override the lock. The terminal lock is removed the next time you start a terminal session to the device.

> All automated processes are suspended while the port is locked by a user.

# Ending a terminal session

End a terminal session by typing **~ [Enter]** on a line by itself.

When you end your session, you will be prompted to enter a comment describing the reason for your changes if changes are detected.

# Using terminal pass-through

If terminal pass-through is enabled on the device, an SSH or Telnet session can be opened directly to the Local Manager while retaining the rollback capabilities, session logging, and authorization checking of the Local Manager. Refer to Configuring SSH or Telnet terminal pass-through protocol for information on configuring terminal pass-through.

Depending on your permissions, you may need to log in to the device.

```
dsmith@central:~$ ssh -p 2001 admin@203.0.113.1 
admin@203.0.113.1's password:
Permission granted for pass-through
Press ~[ENTER] to exit
Connecting ...
```