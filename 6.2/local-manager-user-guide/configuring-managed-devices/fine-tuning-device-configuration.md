# Overview

The assimilation process sets synchronous logging on the managed device console port and configures buffered logging. When you initialize the port, the **config init** dialog prompts you to assimilate the device. If you do not choose to assimilate the device as a part of the initialization, this fine-tuning step can be performed later, either automatically or manually.

# Optimizing the device configuration automatically

The assimilation process is available outside of the **config init** process with the **assimilate** command. 

To change the settings used in the assimilation process, use the **config settings** command.

```
[admin@UplogixLM (port1/1)]# assimilate
Retrieving running-config from device ...
Retrieving running-config from device ...
Removing buffered logging.
Setting logging synchronous.
Retrieving running-config from device ...
running-config saved to archive as current.
```

Assimilate can be undone by issuing the **rollback assimilate** command.

```
[admin@UplogixLM (port1/1)]# rollback assimilate
Retrieving running-config from device ...
Removing buffered logging.
Unsetting logging synchronous.
Retrieving running-config from device ...
running-config saved to archive as current.
```

# Optimizing the device configuration manually
If you choose not to assimilate the device when initializing the Local Manager port to manage the device, you can do so manually as shown below.

## Synchronous logging (Cisco only)

Enabling synchronous logging is done so that device-originated console output is displayed after console output originated by the user or by the Local Manager. For example, if the Local Manager requests a display of the device's running configuration and the device generates console-bound system log messages while the configuration display is in progress, the entire configuration is displayed first, and the system log message is displayed afterward. By default, synchronous logging is used on Cisco devices. Use the **config device logging** command to change this.

```
[admin@UplogixLM (port1/1)]# config device logging
--- Existing  Values ---
Set the console to use synchronous logging: yes
Set the console to use logging buffered: no
Port syslog forwarding enabled: no
Change these? (y/n) [n]: y
--- Enter New Values ---
Set the console to use synchronous logging (y/n) [y]: 
Set the console to use logging buffered (y/n) [n]: y
Logging level for buffered logging (PIX only) [3]: 
Device buffer polling interval [30]: 
Clear device log buffer on poll (y/n) [n]: 
Log buffer clearing needs to be enabled to use forwarding.
Do you want to commit these changes? (y/n): 
```

## Buffered logging

To minimize the load on the network device, turn on buffered logging so the Local Manager can refer to the buffered list of messages. This batch approach operates more efficiently because it requires fewer resources on the device. Use the **config device logging** command to change this.

> Some devices do not support buffered logging. The Local Manager defaults to collecting console log data as it streams to the console.
