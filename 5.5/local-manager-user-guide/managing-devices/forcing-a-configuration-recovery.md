<!-- 5.4 -->

The Local Manager can restore the configuration of a Cisco router or switch that it cannot access because of an authentication or an improperly pushed configuration file. Configuration recovery can recover a password by restoring a previously stored password, along with that configuration.

> This feature is available for Cisco routers running IOS and Cisco switches running CatOS.

The following conditions must be met before the Local Manager can force the configuration recovery:

* A valid device startup configuration must be stored on the Local Manager. One can be manually obtained using the **pull config startup** command.
* The device must be plugged into a power controller that is managed by and appropriately configured on the Local Manager.

The configuration recovery consists of replacing the startup-config on the device with a startup-config stored on the Local Manager.

```
[admin@UplogixLM (port1/4)]# recover configuration
This process can take about 5 minutes.
Attempting to revert startup configuration to current from 10 Jun 21:57
Powering off outlet(s) [1, 2]
DSR was active.
CTS was active.
CTS is still active.
Powering on outlet(s) [1, 2]
Serial link is active.
Attempting to break into ROMmon mode.
Break into ROMmon successful.
Reading post
Image decompressing
Image decompressed
Post complete.
recoverPassword on port1/4 succeeded
```