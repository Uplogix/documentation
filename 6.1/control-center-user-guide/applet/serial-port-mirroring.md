<!-- 5.4 -->

<div class='ucc' />Applet > Terminal > Forward</div>

# Overview

Use the Serial Port Mirroring feature to expose the console port of the managed device available on a local workstation TCP port. This is often used to simulate direct serial port connectivity from workstation to device as if the device was serially directly connected.  A software TCP-to-COM port redirector may be necessary to complete the connection to the application if it requires COM port addressing.  In order to utilize this feature, a user must have the terminal privilege and utilize the SSH Applet on the Control Center.

Prior to setting up serial port mirroring, initialize the Local Manager port with the appropriate device driver via the **config init** command. Refer to the appropriate device configuration guide for information.

# About Connections

* Only one exposed connection is made per mirrored port. Subsequent connections will fail until the first connection is exited.
* The mirror can be terminated by selecting *Terminal*, *Forward* and *Mirror* from the Applet menu and un-checking the *Forward* checkbox.
* Accessing a mirrored port via local application utilizes authentication and authorization previously negotiated.
* Connections to mirrored ports are subject to the same idle timeouts as normal terminal sessions. The idle counter is reset if data is passed over the terminal connection.

# Usage

Start the SSH Applet by navigating to a device in the inventory tree and clicking on the SSH or Dial button. Once the Applet loads, authenticate with the device and log in.

Click on *Terminal* in the SSH Applet menu bar and select *Forward*.

![Uplogix Control Center - Applet Terminal Forward](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-terminal-forward.png))

Mark the checkbox next to mirror. By default, the Applet will forward to a random local port. To specify a port, delete random and enter the desired port.

![Uplogix Control Center - Applet Terminal Forward Mirror](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings-mirror.png)

Click *Apply* to save your settings. If a random port was assigned, it will be displayed and highlighted in green.
 
Click *Close* to return to your Applet session.

Anything typed to the mirrored port will be displayed in the original terminal session.
