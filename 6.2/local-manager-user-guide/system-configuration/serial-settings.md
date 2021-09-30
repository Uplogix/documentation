<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary > System > Serial</div>

<div class='warning' />**Deprecated.** This command is only available on the Uplogix 400/430/3200 Local Managers.</div>

The default management console connection settings for the Local Manager are 9600 baud, 8 data bits, 1 stop bit, no parity, and no flow control.

> By default, Windows HyperTerminal uses hardware flow control. The Uplogix 430 Local Manager does not use flow control. If using HyperTerminal with the Uplogix 430 Local Manager, flow control must be disabled when configuring the session.

The mini-USB console ports on the 500/5000 platforms are enabled in 5.1 for the Windows operating system (Windows 7). See [Connecting to USB Console Port in Windows 10](http://uplogix.com/docs/local-manager-user-guide/introduction/connecting-to-usb-console-windows-10).

The console ports for the Local Managers accept standard RS-232 serial cables with RJ-45 connectors configured as **DCE** unless otherwise labeled or configured. The Uplogix 400 and 3200 can be configured to use null modem cables by rolling the TX/RX connections in hardware.

The Uplogix 430 Local Manager is shipped with its own console cable.

To use a null modem cable with an Uplogix 400 or 3200, use the **config system serial** command and enable the null modem setting if it was not enabled during initial configuration when the Local Manager was installed.

```
[admin@UplogixLM]# config system serial
--- Existing Values ---
Null modem: no
Change these? (y/n) [n]: y
Enable null modem? (y/n) [n]: y
Do you want to commit these changes? (y/n): y
```