<!-- 5.4 -->

Each port has a set of parameters that control interactions with the device it manages. You can define file transfer methods and priorities, configure file save method, wait time during device reboots, and so forth. These are the settings applied during the assimilation process, which fine-tunes the device settings for optimum performance.

The factory default settings for the Local Manager represent common industry practices, but your environment may require customized settings.

To access port settings, use the interactive **config settings** command. Each entry in the settings list is accessed by entering the number associated with that entry.

```
[admin@UplogixLM (port1/1)]# config settings
--- Settings Menu ---
1 Assimilated terminal speed: 19200
2 Modify terminal serial speed on assimilation: false
3 Device configuration pull method: tftp
4 Device configuration push method: xmodem
5 Alternative device configuration push method: tftp
6 Device configuration push retries: 3
7 Automatic configuration rollback: [disabled/manual/automatic] manual
8 Count delay before automatic configuration rollback: 75
9 Issue 'write memory' after configuration rollback: true
10 Verify OS upgrade: true
11 Use manual boot during upgrade, if applicable: true
12 OS image push method: tftp
13 Alternative OS image push method: xmodem
14 Attempt to use XModem-1K (first attempt only): true
15 Save Configuration on change before reboot? true
16 Include current running-config in exports? true
17 Previous OS image not found, continue? true
18 Maximum OS image push retry attempts: 3
19 Device reboot timeout (seconds): 300
20 Force the device to reboot immediately after pushing the OS: true
21 Device pass through timeout(seconds): 300
22 Enable local echo: false
23 Leave old OS if space permits during OS upgrade: true
24 Pull config before 'terminal' if local copy is older than (minutes)? 6
25 Done
Select setting to edit or 25 to end: 
```

After the setting is modified, the full list of settings is displayed again, with your change.

<div class='ucc' />Inventory > Local Manager Summary >Â System > Default Port Settings</div>

|Item	|Setting|	Description|
|:---|:---|:---|
|1|Assimilated terminal speed|Define the assimilated terminal speed. Options: 300, 600, 1200, 2400, 4800, **9600**, 19200, 38400, 57600 or 115200
|2|Modify terminal serial speed on assimilation|Allows the Local Manager to change the terminal speed of the managed device during assimilation. Options: True or **False**. |
|3|Device configuration pull method|Defines the method the Local Manager will use to pull configuration information from the managed device. Options: **TFTP**, console, or FTP|
|4|Device configuration push method|Defines the method the Local Manager will use to push configuration information to the managed device. Options: TFTP, console, **xmodem**, or FTP|
|5|Alternative device configuration push method|Defines a secondary method the Local Manager will use to push configuration information to the managed device if the primary method fails. Options: **TFTP**, console, xmodem, or FTP|
|6|Device configuration push retries|Number of retry attempts the Local Manager will make to push a configuration to a managed device. Options: Integer value|
|7|Automatic configuration rollback|Enable, disable or change SurgicalRollbackâ„¢ settings. Options: **manual**, disabled, or automatic|
|8|Count delay before automatic configuration rollback|Set the delay (in seconds) the Local Manager will wait before initiating SurgicalRollbackâ„¢ if that feature has been set to run automatically. Options: Integer value|
|9|Issue 'write memory' after configuration rollback|Define if the Local Manager will perform a â€˜write memoryâ€™ on a device after a configuration has been rolled back. Options: **True** or False|
|10|Verify OS upgrade|Define if the Local Manager will verify the managed device successfully upgraded. Options: **True** or False|
|11|Use manual boot during upgrade, if applicable|Define if the Local Manager will manually boot the managed device during the course of a scheduled upgrade. Options: **True** or False|
|12|OS image push method|Defines the method the Local Manager will use to push an OS image to the managed device. Options: **TFTP**, ymodem, xmodem, or FTP|
|13|Alternative OS image push method|Defines a secondary method the Local Manager will use to push an OS image to the managed device if the primary method fails. Options: TFTP, ymodem, **xmodem**, or FTP|
|14|Attempt to use XModem-1K (first attempt only)|Defines if XModem-1K will be used in the first attempt of a pull or push activity. Options: **True** or False|
|15|Save Configuration on change before reboot?|Defines if a managed device configuration will be saved if there is a change and the user has issued a reboot. Options: **True** or False|
|16| Include current running-config in exports. | Defines if the device's running-config is included when **config export** is enabled. Options: **True** or False |
|17|Previous OS image not found, continue?|Defines if the Local Manager will push a new OS image if a previous version is not stored locally. Options: **True** or False|
|18|Maximum OS image push retry attempts|Defines the number of attempts the Local Manager will retry a push OS operation after it has initially failed. Options: Integer value|
|19|Device reboot timeout (seconds)|Defines wait time during a managed device reboot. Options: Integer value|
|20|Force the device to reboot immediately after pushing the OS|Defines if the Local Manager will reboot the managed device after an OS is pushed to it. Options: **True** or False|
|21|Device pass through timeout (seconds)|Defines the inactivity timeout of a terminal session on the managed device. Options: Integer value|
|22|Enable local echo|Enables or disables local echo on a managed device. Options: True or **False**|
|23|Leave old OS if space permits during OS upgrade|Determines what the Local Manager will do with the old OS file(s) on a managed device during an OS upgrade. Options: **True** or False|
|24|Pull config before **terminal** if local copy is older than (minutes)?| If the local copy of the configuration is recent, do not pull another copy before **terminal**. Options: Integer value |
|25|Done|Saves changes made and exits the port settings wizard|

# Most Frequently Used

## Option 7 - Automatic Rollback Configuration

Defines whether the Local Manager automatically rolls back uncommitted configuration changes on a managed device. Available options are *disabled*, *manual*, and *automatic*.

### Disabled

If Automatic Rollback is disabled, no running configurations are pulled, hence no changes are determined or presented.

### Manual (default)

In this mode, the configuration is pulled prior to the **terminal** command (dependent on Option 24). After the **terminal** session, the configuration is pulled again. The user is presented with a list of the changes made during the session.

```
Disconnecting ...

Logging out of device...
Attempting to retrieve configuration using the console...
Complete. running-config pulled.
running-config saved to archive as current.

Changes made in current terminal session: 
+hostname HOU-CORE
-hostname AUS-CORE
```

To roll back the changes manually, use the **rollback config** command.

```
[admin@UplogixLM (port1/1)]# rollback config
Retrieving running-config from device ...
Complete. running-config pulled.

Transferring via XModem.
Initiating file transfer
Transferring file ...

Sent staging-running-config (43 bytes) at 121 B/s.

File staging-running-config was transferred to the device successfully via XModem.
staging-running-config copied to running-config
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
Rollback successful.
running 'write memory'
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
```

### Automatic

Similar to Manual mode, except that after changes are shown to a user, a countdown begins.

```
Changes made in current terminal session: 
+hostname HOU-CORE
-hostname AUS-CORE

Warning: Automatic rollback in effect.
Any changes to the device's running-config will be restored in 75 seconds.
75  seconds remaining. ([C]ommit/[P]ostpone/[R]ollback immediately):
```

If a user is disconnected during the **terminal** session or during the rollback countdown, the configuration is immediately rolled back. 

```
Warning: Automatic rollback in effect.
Any changes to the device's running-config will be restored in 75 seconds.
1  seconds remaining. ([C]ommit/[P]ostpone/[R]ollback immediately):
Rolling back changes to running-config...
```

## Option 21 - Device pass through timeout

Users can be automatically logged out of **terminal** sessions if they are idle too long. Specify a max idle time in seconds. The user will be presented with a warning message when half of the idle time has expired.

```
Console session started.  Press ~[ENTER] to exit.


AUS-CORE#

You have been idle for 150 seconds. Your session will end in 150 seconds.
```

When the full timer expires, the user will be logged out. If Automatic Rollback is in effect, any changes made during the session will be undone.

```
You have been idle for 300 seconds, your session is ending.



Disconnecting ...

Logging out of device...
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
```

<!-- Add td width 50px to first th in config settings tables -->