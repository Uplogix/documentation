<!-- 5.4 -->

This feature enables access to network services running on the dedicated or management IP addresses of a managed device. Multiple users on multiple workstations can use SSH Port Forwarding concurrently.

Certain privileges are required to edit or view a portâ€™s forward configuration.

* **show protocols forward** â€” Views the forwarding settings.
* **config protocols forward** â€” Configures the forwarding settings.
* **forward** â€” Allows the user to open an SSH session with a tunnel to the forwarded port.

The Local Manager will attempt to forward incoming TCP traffic regardless of whether the destination is configured properly or not. Ensure the managed device is configured to listen on the port specified.

Complete the following steps to configure SSH port forwarding for your managed device.

# Configure IP Addresses

The managed deviceâ€™s management or dedicated IP address must be configured on the Uplogix device. This can be configured using **config init** or **config info**.

```
[admin@UplogixLM (port1/1)]# config init
--- Enter New Values ---
description: []:
////
management IP: []: 192.0.2.200
Configure dedicated ethernet port? (y/n) [y]:
Use DHCP? (y/n) [n]:
dedicated device IP []: 192.0.2.2
dedicated port IP []: 192.0.2.1
dedicated netmask: []: 255.255.255.252
speed/duplex: [auto]:
////
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

**[no] management {port}**

Enables forwarding to the management IP address and the port specified. The no prefix will remove the forward.

Example: To enable traffic forwarding to port 80 on the managed deviceâ€™s management IP address, use management 80.

**[no] dedicated {port}**

Enables forwarding to the dedicated IP address and the port specified. The no prefix will remove the forward.

Example: To enable traffic forwarding to port 80 on the managed deviceâ€™s dedicated IP address, use dedicated 80.

**[no] events**

Turns on event logging for traffic forwarding. The no prefix will turn off event logging.

**show**

Displays the current configuration.

**exit**

Exits the configuration editor.

> The port specified should match the listening port on the managed device. If the managed device is running an SSH server on its management IP address, forwarding should be configured as management 22.

# Creating a Tunnel

When connecting with an SSH client, you can specify an IP address or hostname and a port to create a tunnel. With forwarding enabled, the Uplogix device will allowing incoming users to establish a tunnel for which they have the forward privilege.

Hostnames will take the form of portx_y. For example, â€œport 1/1â€ will be specified as â€œport1_1â€ when creating the tunnel. This hostname will point to whichever IP address is configured for forwarding, either management or dedicated. If both addresses are configured for forwarding, an IP address should be used to avoid ambiguity.

# SSH Client Examples

Below are examples of how to set up this feature using OpenSSH and PuTTY. For an example of this feature using the Control Center CLI Applet, refer to the Uplogix Control Center Users Guide.

## OpenSSH (Linux/Unix)

The ssh command on most Linux platforms provides for port forwarding with the â€“L option. For example, if port 1/3 is forwarding port 80 on its dedicated IP address and you want to map it locally to port 1080, use the following command:

```
ssh â€“L 1080:port1_3:80 username@uplogixlocalmanager
```

An IP address can also be used:

```
ssh â€“L 1080:192.0.2.40:80 username@uplogixlocalmanager
```

## PuTTY

Open PuTTY, enter an IP address (1), and then select Tunnels under Category > SSH (2).

![PuTTY - IP and Tunnels](http://uplogix.com/support/docs/img/5.4/putty-ip-tunnels.png)

Configure port forwarding with the following options:

(1) Source Port: A local port on the userâ€™s workstation to forward the remote port to. For example, to make the remote port 80 appear locally as 1080, use 1080 as the source port.

(2) Destination: A combination of the destination hostname (or IP address) and the remote port. For example, to create a tunnel to port 80 on port 1/1, use port1_1:80. If you would like to specify the IP address, use 192.0.2.1:80 (where 192.x.x.x is the management or dedicated IP address of the managed device).

The default options of Local and Auto will be sufficient for creating the tunnel.

(3) Click Add to save the configuration for use with the next SSH connection. 

![PuTTY - SSH Port Forwarding](http://uplogix.com/support/docs/img/5.4/putty-ssh-port-forwarding.png)

Once you click Open and establish a session, the tunnel will be created.

In this example, you would then be able to open a web browser to http://127.0.0.1:1080. Your request will be forwarded through the tunnel to the managed device on port 1/1.

# Notes

Access to forwarded ports is secured by mapping the requested hostname or IP address to a managed device on the Local Manager. If forwarding is enabled for two ports that have the same management or dedicated IP addresses, it may be possible for a user to access the forwarded port of a device that they do not have explicit permission for.

Any tunnels created with an SSH session will be torn down if the session times out or is exited. To regain access to the tunnel, initiate another SSH session.