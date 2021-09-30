<!-- 5.4 -->

<div class='ucc' />Applet > Terminal > Forward</div>

# Overview

Use the Serial Port Forwarding feature to make the console port of the managed device available on a local workstation via reverse SSH tunnel. In order to utilize this feature, a user must have the **terminal** privilege.

An SSH client with reverse tunnel capabilities is required to use this feature. Supported clients include PuTTY and the CLI Applet on the Control Center.

Prior to setting up serial port forwarding, initialize the Local Manager port with the appropriate device driver via the **config init** command. Refer to the appropriate device configuration guide for information. 

# About Connections

* Only one TCP connection is allowed per forwarded port. Subsequent connections will fail until the first connection is exited.
* The TCP connection can be terminated by disabling the forward setting in the SSH Applet or by closing the SSH client.
* Connections to forwarded ports are subject to the same idle timeouts as normal terminal sessions. The idle counter is reset if data is passed over the TCP connection.

# Usage

Start the SSH Applet by navigating to a device in the inventory tree and clicking on the SSH button. Once the Applet loads, authenticate with the device and log in.

Click on *Terminal* in the SSH Applet menu bar and select *Forward*.

![Uplogix Control Center - Applet Terminal Forward](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-terminal-forward.png)

Mark the checkbox next to the port you wish to forward. By default, the applet will forward to a random local port. To specify a port, delete random and enter the desired port.

![Uplogix Control Center - Applet Forward Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings.png)
 
Click *Apply* to save your settings. If a random port was assigned, it will be displayed and highlighted in green.

![Uplogix Control Center - Applet Forward Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings-applied.png)
 
If you specified an invalid port (in use or conflicting), it will be highlighted in red.

![Uplogix Control Center - Applet Forward Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings-invalid.png)

Click *Close* to return to your SSH session.

Navigate to the desired port and use the **terminal forward** command to start forwarding.

![Uplogix Control Center - Applet Terminal Forward](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-terminal-forward-cli.png)
 
Once the message *Console session forwarded* displays, connect to the forwarded session on your local machine. Navigate to 127.0.0.1 (localhost) on the port specified earlier using your workstation application such as a browser or element manager.

Anything typed to the forwarded port will be displayed in the original terminal session.