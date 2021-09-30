# Overview

When connecting managed devices to the dedicated Ethernet ports of the Local Manager, you can configure their dedicated Ethernet connections to use static IP addresses or acquire DHCP addresses from the Local Manager.

> Dedicated Ethernet requires an Ethernet option card on the Uplogix 5000 or 83X platform.

When setting the Local Manager to assign DHCP addresses to devices, the DHCP pool must not overlap with other pools or subnets:

 - the base address must not overlap the system's management IP address
 - the base address must not overlap existing static assignments on ports

<div class='warning' /> If these requirements are not met, the Local Manager will not assign addresses properly and Ethernet-related features will be unavailable. </div>

Use the **config system protocols dhcp** command to set the base DHCP address that will be used in generating addresses.

The syntax for this command is: **config system protocols dhcp [nnn.nnn.nnn]** where nnn.nnn.nnn is the base address to be used. The default base address is 169.254.100.

For example:

```
[admin@UplogixLM]# config system protocols dhcp 192.168.1

[admin@UplogixLM]# show system protocols dhcp
Server DHCP base address: 192.168.1
-- OUTPUT REMOVED --
```

The devices connected to individual ports must also be configured to use DHCP. When configuring a device on a port using the **config init** command, the dialog asks whether to configure a dedicated Ethernet port. If you respond with **y**, the next prompt asks whether to use DHCP. 

```
Configure dedicated ethernet port? (y/n) [n]: y
Use DHCP? (y/n) [n]: y
```

If the device is configured to use DHCP, it is not accessible until it requests a DHCP address.

Changes to the **config system protocols dhcp** setting take effect after restarting the Local Manager.

<div class='ucc' />Inventory > Local Manager Summary Page > Network > Protocols > DHCP Server Settings</div>

# Using Dedicated Ethernet with Switches

For a switch configured to use a dedicated Ethernet port with a static IP address, the Local Manager turns off the interface except when it is needed. When the Local Manager turns on the dedicated Ethernet port, it can take 30-50 seconds for the switch to start forwarding traffic if the Spanning Tree Protocol (STP) is running on the switch port.  Uplogix recommends using a feature like Cisco's portfast STP feature when connecting a switch port to a Local Manager dedicated Ethernet port.

Sometimes, actions that result in a pull OS operation (such as using the **copy** command) may return messages that FTP has failed, because the pull operation starts before the interface is ready. The pull operation then succeeds when the pull is attempted using its secondary transfer method. *This issue is unique to switches using dedicated Ethernet ports with static IP addresses where the Spanning Tree Protocol is running on the switch port.*

If the dedicated Ethernet port uses DHCP, the interface remains up during normal operation.

There are two ways to prevent the problem:

 - Configure the dedicated Ethernet connection to use DHCP (not available for Uplogix  500 Local Managers)
OR
 - Enable the portfast feature on Cisco switch ports - see following configuration example:
 
```
interface FastEthernet1/0/1
description dedicated Ethernet to Local Manager
switchport access vlan 2
spanning-tree portfast
```