# Overview
Some manual configuration changes to an operational device can cause it to drop the command	line connection. You can undo the changes from a terminal session without reapplying the entire running configuration, either with the automatic  SurgicalRollbackâ„¢ feature or with a manually initiated rollback.

Both rollback features return the device to the state immediately before the changes, reducing time to recovery as well as the time needed for contingency planning.

When using the **terminal** command or a terminal pass-through session to access a device, the Local Manager retrieves the device's running configuration. After exiting the terminal session and returning to the command line, the Local Manager retrieves another copy of the running configuration. The Local Manager compares the two running configurations and creates a difference file. Both rollback methods undo the changes in the difference file without reapplying the entire running configuration or rebooting the managed device.

The **config settings** command specifies rollback transfer methods (XMODEM, TFTP, FTP).

The rollback capability is only available when using a terminal session from the Local Manager to access the device (note: changes made to a device via a SSH session to the managed device that bypasses the Local Manager cannot be rolled back). This feature can only roll back changes from the most recent terminal session. Entering and exiting the device via the terminal command constitutes a session. For example, if you access the device using the terminal command, change the hostname, and exit the terminal session; then terminal in again, issue a show version command and exit, you will not be able to use either automatic SurgicalRollbackâ„¢ or manually initiated rollback to undo the hostname change, as it was not done during the most recent session.

>Scheduled tasks and monitors do not affect rollback.

# Undoing changes automatically with SurgicalRollbackâ„¢ 

SurgicalRollbackâ„¢ is the default behavior when ending a terminal session. If the Local Manager notes configuration changes during a terminal session, it displays the changes along with a message warning that your changes will be rolled back if you donâ€™t commit the changes. The Local Manager prompts you to commit your changes, postpone rollback, or roll back the changes immediately. If you do not respond within 75 seconds, the rollback takes place by default. During the countdown to rollback, the Local Manager sends the ASCII bell character each time it refreshes the countdown display, to provide an audio cue that rollback is about to start.

If you need more time to review the list of changes, you can delay SurgicalRollbackâ„¢ by typing **p** to postpone the process for the number of seconds that you specify.

The following example shows a configuration change and the difference document that the Local Manager creates.

```
[admin@UplogixLM (port1/1)]# terminal
Press "~[ENTER]" to exit
Connecting ...
Retrieving running-config from device ...
Complete. running-config pulled.
Cisco7206#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Cisco7206(config)#hostname Demo7206
Demo7206(config)#access-list 101 permit pim any 192.0.2.0 0.0.0.255 tos min-delay
Demo7206(config)#exit
~[enter]
Disconnecting ...
Retrieving running-config from device ...
Complete. running-config pulled.
Changes made in current terminal session:
+hostname Demo7206
-hostname Cisco7206
+access-list 101 permit pim any 192.0.2.0 0.0.0.255 tos min-delay

Warning: Automatic rollback in effect.
Any changes to the device's running-config will be restored in 75 seconds.
70 seconds remaining. ([C]ommit/[P]ostpone/[R]ollback immediately):
```

In the example above, after return to the command line, the Local Manager identifies configuration changes listed and begins a countdown to automated configuration rollback.

Lines that are removed are prefixed with the **â€“** character.

Lines that are added are prefixed with a **+** character.

# Undoing changes with a manually initiated rollback

If you commit the changes from a terminal session but then decide they should be rolled back, start a rollback procedure manually. To see the list of changes that will be made, use the **show rollback-config** command. For example, if you completed the terminal session shown above and committed the changes, the following would display:

```
[admin@UplogixLM (port1/1)]# show rollback-config
!
no hostname Demo7206
no access-list 101 permit pim any 192.0.2.0 0.0.0.255 tos min-delay
hostname Cisco7206
!
```

To make the changes listed, use the **rollback config** command.

This capability is available for some but not all types of managed devices.