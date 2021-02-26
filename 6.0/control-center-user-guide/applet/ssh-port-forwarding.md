<!-- 5.4 -->

<div class='ucc' />Applet > Terminal > Forward</div>

# Overview

SSH port forwarding enables access to network services running on the dedicated or management IP addresses of a managed device. Multiple users on multiple workstations can use SSH Port Forwarding concurrently.

Certain privileges are required to edit or view a portâ€™s forward configuration:

* **show protocols forward** - Views the forwarding settings.
* **config protocols forward** - Configures the forwarding settings.
* **forward** - Allows the user to open an SSH session with a tunnel to the forwarded port.

The Local Manager will attempt to forward incoming TCP traffic regardless of whether the destination is configured properly or not. Ensure the managed device is configured to listen on the port specified.

When using the SSH Applet on the Control Center, a Java Runtime Environment (JRE) must be installed on the userâ€™s workstation.

# Usage

First, connect to the web interface of the Control Center and navigate to the Inventory page. Select a Local Manager from the Inventory tree to bring up its detail page. Launch the Control Center applet by clicking on the **SSH** button.
â€ƒ
# Configure IP Addresses

The managed deviceâ€™s management or dedicated IP address must be configured on the Local Manager. This can be configured using **config init** or **config info**.

```
[admin@UplogixLM (port1/1)]# config init
--- Enter New Values ---
description: []:
<output removed>
management IP: []: 198.0.2.100
Configure dedicated ethernet port? (y/n) [y]:
Use DHCP? (y/n) [n]:
dedicated device IP []: 169.254.100.2
dedicated port IP []: 169.254.110.3
dedicated netmask: []: 255.255.255.252
speed/duplex: [auto]:
<output removed>
Do you want to commit these changes? (y/n): y
```

# Configure Port Forwarding

Use the **config protocols forward** command to open the port forwarding configuration editor.

```
[admin@UplogixLM (port1/1)]# config protocols forward
[forward]#
```
Once in the editor, you can use the ? command to view a list of possible options.

```
[forward]# ?
Forward options are:
[no] management {port}
[no] dedicated {port}
[no] events
show
exit
```

* **[no] management {port}** - Enables forwarding to the management IP address and the port specified. The **no** prefix will remove the forward.

 Example: To enable traffic forwarding to port 80 on the managed deviceâ€™s management IP address, use **management 80**.

* **[no] dedicated {port}** - Enables forwarding to the dedicated IP address and the port specified. The **no** prefix will remove the forward.

 Example: To enable traffic forwarding to port 80 on the managed deviceâ€™s dedicated IP address, use dedicated 80.

* **[no] events** - Turns on event logging for traffic forwarding. The **no** prefix will turn off event logging.
* **show** - Displays the current configuration.
* **exit** - Exits the configuration editor.

Note that the port specified should match the listening port on the managed device. If the managed device is running an SSH server on its management IP address, forwarding should be configured as management 22.

# Creating a Tunnel

To use the SSH Applet on the Control Center, navigate to a device in the Inventory tree and click on the *SSH* button. Once the Applet has loaded, click on *Terminal* in the menu bar and select *Forward*.

![Uplogix Control Center - Terminal Forward Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings.png)

In this example, the Local Manager has already been configured to forward traffic to port 22 at the management IP address for the device on port 1/2. The screen above allows you to select which tunnels to create. On a device with multiple forwards configured, the above list would be longer.

To create a tunnel, check the box next to the port forwards you wish to enable. Then, select a local port to use for forwarding. If random is selected, the applet will select a random port on the workstation. Click *Apply* to save your settings.

![Uplogix Control Center - Applet Forward Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings-applied.png)
 
If the forward was successful, the drop down box will turn green. If a random port was requested, the port number will be displayed in the green box.

![Uplogix Control Center - Applet Forward Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-applet-forward-settings-invalid.png)
 
If the drop-down menu turns red, this indicates the local port was unavailable and the tunnel was not created. Choose a different local port that is not currently in use. 

# Notes

* Access to forwarded ports is secured by mapping the requested hostname or IP address to a managed device on the device. If forwarding is enabled for two ports that have the same management or dedicated IP addresses, it may be possible for a user to access the forwarded port of a device that they do not have explicit permission for.
* Any tunnels created with an SSH session will be destroyed if the session times out or is exited. To regain access to the tunnel, initiate another SSH session.