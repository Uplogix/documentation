<!-- 5.4 -->

# Overview

The Uplogix Control Center provides a full-featured SSH applet for interaction with Local Managers. If configured properly, the SSH applet can also automatically dial a Local Manager via its out-of-band connection. 

The SSH button can be found on the Local Manager Summary page in both the header and Appliance overview section. Clicking either of these buttons will open an SSH session with the Local Manager. Once you have authenticated with the LM, you will be logged into the system resource.

> Prior to version 5.4, the SSH Applet was known as the CLI Applet.

### Version 5.4 and later

![Uplogix Control Center - SSH Applet Button](http://uplogix.com/support/docs/img/6.0/ssh-applet-button.png)

### Version 5.3 and earlier

![](http://uplogix.com/support/docs/img/ucc5.2/applet_system.png)

SSH buttons are also available on other resources, including ports, modem, and power controller. Clicking the SSH button next to one of these resources will open an SSH session with the Local Manager. Once you have authenticated, you will bypass the system resource and be placed directly in a terminal session with the managed device.

> Terminal commands are still available. Type ~h for a list of available commands.

# Java Requirements

As of LMS version 5.2, the SSH Applet has been updated to no longer run as a Java applet in your browser. Instead, it runs as a desktop application using the Java Network Launch Protocol (JNLP). This requires the latest version of the Java Runtime Environment (JRE) to be installed on your computer.

Clicking on an SSH or DIAL button will now download a JNLP file to your workstation. If this file type is properly associated with Java (which should happen automatically during the installation of the JRE), it will automatically launch the CLI applet. 

To download the latest JRE, visit [java.com/download](http://java.com/download).

The first time a user launches the CLI Applet in LMS version 5.2 or later, they will see the following notice:

![](http://uplogix.com/support/docs/img/rob/Uplogix-Java-Applet.png)

# Routing Requirements

Since the SSH Applet runs locally from the user's workstation, a valid route must be available to SSH directly to the Local Manager. The SSH session *does not* originate from the Control Center by default, so even if the Control Center and Local Manager are communicating successfully, the workstation still needs to be able to route directly to the Local Manager.

## No Route to Host

In cases where network configuration will not allow for direct routing, a SOCKS Proxy can be used to route the SSH session. The SSH Applet can automatically connect to the SOCKS Proxy and then initiate the connection to the Local Manager. See *[SS5 SOCKS Proxy](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/ss5-socks-proxy)* for more information.

## Non-Routable Networks

If the target Local Manager is behind a NAT, it will still report its private IP address to the Control Center. If the SSH button is clicked, the SSH session will be opened to the private address, and the connection will fail. You can use *Properties* to override with the Local Manager's IP address with a new one.

The following properties are available:

* **sshIp** - This property will override the reported IP address when initiating an SSH connection with the SSH applet. For example, if the Local Manager's IP is 192.168.1.14, but sshIp is configured as 75.125.200.98, clicking on the SSH applet will open connection to 75.125.200.98. Useful if an appliance is behind a firewall or NAT.

* **sshPort** - This property overrides the default port 22 for SSH connections. Useful if the Local Manager is behind a router with port forwarding capabilities.

* **sshIpv6** - Specifies an alternate IPv6 address to be used instead of the address reported by the Local Manager.

* **sshIpOob** - This property will override the reported Out of Band IP address. Useful if an appliance ends up behind a firewall or NAT when it brings up its out of band connection.

* **sshPortOob** - This property overrides the default port 22 for SSH connections while the Local Manager is operating Out of Band.

* **sshIpv6Oob** - Specifies an alternate IPv6 addressed to be used when the Local Manager is operating Out of Band.

# Features

Additional functionality can be accessed via the *Terminal* and *Edit* menus in the SSH applet.

## Terminal

**Connect** - Connects to the Local Manager. Can be used after *Disconnect* or during an active session to restart it.

**Forward** - Provides forwarding of remote serial ports to local TCP ports on the workstation. For example, Port 1/1 could be forwarded to port 20001 of 127.0.0.1 (localhost). The terminal session would then be accessible by opening a Telnet connection to 127.0.0.1 on port 20001. This feature is used most often with GUI applications that require terminal access to managed devices.

**Reset** - If the CLI text becomes garbled during interaction with a managed device, use the *Reset* command to reset the terminal session. 

**Disconnect** - Disconnects the current session.

## Edit

**Copy** - Copies text to the clipboard.

**Paste** - Pastes text from the clipboard.

**Preferences** - Configure SSH Applet preferences.

* Appearance - Change the font, style, size, and color of the SSH Applet text.
* Logging - Enable debug and session logging
* Scrolling - Specify the buffer size for scrollback
* Private Key - Install an SSH key. 