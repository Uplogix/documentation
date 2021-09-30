<!-- 5.4 -->

Multiple subinterfaces can be configured on the management Ethernet interface.

# Usage Notes

* SLV traffic can now be directed to specific VLANs on the Local Manager Ethernet management interface (i.e. subinterfaces), enabling synthetic SLV traffic to follow the same path through the network as the real traffic being simulated/measured.
* Multiple network interfaces can now be defined (i.e. interfaces on different VLANs), allowing users to log into the Local Manager from non-management VLANs.
* Some networks local to the Uplogix LM may not be reachable through the out-of-band network. Static routes can now be created on the management interface to force traffic on the Uplogix LM destined for these local networks to use the in-band Ethernet interface when routing to these specific local networks that would not be reachable over the out-of-band network.

# Requirements

* This feature requires the Ethernet management interface connection for the Uplogix Local Manager to be an 802.1Q trunk. 
* The Uplogix Local Manager must be enabled with a SLV license in the Uplogix Control Center for IPT configuration

# Configuring a Subinterface

Use the **config system subinterface {subinterface_name}** command to open the subinterface configuration editor.

```
[admin@UplogixLM]# config system subinterface voice
Subinterface voice does not exist. Create (y/n): y
Warning: Remote connections may be lost if you commit changes.
[config subint voice]# 
```

Once in the editor, you can use the **?** command to view a list of possible configuration options.

```
[config subint voice]# ?
Allowable arguments are:
show
description
vlan
[no] ip
[no] ipv6
[no] route
[no] gateway
or 'exit' to quit config mode
```

The following commands are available:

**show**

Display the current subinterface configuration.

**description**

Describe the purpose of the subinterface.

Example: description Voice VLAN for SLV IPT traffic

**vlan {vlan_number}**

Define the VLAN associated with the subinterface.

Example: To associate the subinterface with VLAN=51, use** vlan 51**.

**[no] ip {dhcp | IPv4_address/netmask_bits}**

Set the IPv4 address for the subinterface. The no prefix will remove the IP address from the subinterface.

Example: To set to a class C IPv4 address of 172.30.51.2, use **ip 172.30.51.2/24**. To set the subinterface to DHCP an IP address, use **ip dhcp**.

**[no] ipv6 {IPv6_address/netmask_bits}**

Set the IPv6 address for the subinterface. The no prefix will remove the IP address from the subinterface.

Example: To set the IPv6 address to 2001&#58;100&#58;b951&#58;600&#58;1293&#58;e8f1&#58;fe0b:4932 with a prefix length of 64, use** ipv6 2001&#58;100&#58;b951&#58;600&#58;1293&#58;e8f1&#58;fe0b:4932/64**.

**[no] route {IPv4_address/netmask_bits | IPv6_address/netmask_bits }**

Set an IPv4 or IPv6 static route to be associated with this subinterface. The no prefix will remove the static route from the subinterface.

Example: To route all outgoing traffic headed to the 10.0.1.0/24 network over this subinterface, use route 10.0.1.0/24. To route all outgoing traffic headed for 2001&#58;100::0/32, use route 2001&#58;100::0/32.

**[no] gateway {IPv4_address | IPv6_address}**

Set the IPv4 or IPv6 gateway for this subinterface. The no prefix will remove the gateway address from the interface.

Example: To set the IPv4 gateway to 172.30.51.254, use gateway 172.30.51.254. To set the IPv6 gateway to 2001&#58;100&#58;b951&#58;600&#58;1222&#58;ab71&#58;fe01:2386, use **gateway** **2001&#58;100&#58;b951&#58;600&#58;1222&#58;ab71&#58;fe01:2386**.

**exit**

Exit the configuration editor.

# Display a Subinterface

Use the **show system subinterface {subinterface_name}** command to view the subinterface configuration for a particular subinterface, or use **show system subinterface \* ** to display the configuration for all subinterfaces on the Local Manager.

```
[admin@UplogixLM]# show system subinterface voice
name voice
vlan 51
description Voice VLAN for SLV IPT traffic
ip 172.30.51.2/24
gateway 172.30.51.254
ipv6 2001:100:b951:600:1293:e8f1:fe0b:4932/64
gateway 2001:100:b951:600:1222:ab71:fe01:2386
route 10.0.1.0/24
route 2001:100:0:0:0:0:0:0/32
```

# Delete a Subinterface

Use the **config system subinterface no {subinterface_name}** command to delete specified subinterface. Here is an example that deletes a subinterface named "voice."

```
[admin@UplogixLM]# config system subinterface no voice
```