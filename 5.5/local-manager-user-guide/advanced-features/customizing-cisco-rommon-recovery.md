<!-- 5.4 -->

This section describes how to tailor Cisco NVRAM variables used by the Uplogix Cisco advanced driver when it needs to recover the OS image from ROMmon. More specifically, this allows you the ability to customize the variable settings used by the TFTPDNLD command when the Local Manager finds a router or switch in ROMmon and determines that the OS image needs to be recovered on the Cisco device.

You can customize the following ROMmon variable settings relevant to TFTPDNLD: IP address, subnet mask, default gateway, Ethernet interface, Ethernet interface speed, and duplex settings that override derived and default settings used by the Uplogix driver. For more information on Ciscoâ€™s ROM Monitor and recovering a system image using TFTPDNLD, refer to Ciscoâ€™s Troubleshooting and Maintenance: Using the ROM Monitor documentation for the 1800/2800/3800 Series Integrated Services Routers or the 1900/2900/3900 Series Integrated Services Routers.

# Usage Notes

Customizing ROMmon variable settings adds value in the following situations:

* TFTPDNLD must take place over an Ethernet interface that is not the lowest numbered interface on the device.
* TFTPDNLD uses an interface that is not in the same subnet as the Local Manager Ethernet management interface and which is not a dedicated Ethernet connection to the Local Manager.
* TFTPDNLD uses an Ethernet interface that requires a specific speed and duplex setting in order to work properly from ROMmon.

#Feature Limitations

* This feature is limited to Cisco routers and the switches that support the TFTPDNLD command in ROMmon.
* This feature may not work on all Cisco routers and versions of IOS. Check the Cisco website to validate support for these ROMmon variables.

# Required Privileges

* **config properties** â€” Configure properties on an Local Manager port.
* **show properties** â€” View properties on an Local Manager port.

# Configuring ROMmon Variable Settings

The Uplogix advanced driver recovery from ROMmon functionality only works on Cisco devices that support the TFTPDNLD feature to download an OS image while in ROMmon. This feature utilizes Local Manager port properties to allow defining ROMmon variable settings that should be set by the Uplogix advanced Cisco IOS driver when it attempts to transfer an OS image to the router that is in ROMmon. Any user-defined ROMmon variable settings will override default settings used by the Uplogix LM.

The following ROMmon variables apply to all routers:

 1. IP_ADDRESS â€” IP address of the router
 2. IP_SUBNET_MASK â€” subnet mask of the router
 3. DEFAULT_GATEWAY â€” default gateway of the router

For routers with Fast Ethernet interfaces, the following ROMmon variables should be available to indicate which Fast Ethernet port should be used, as well as the speed and duplex setting for that interface:

1. FE_PORT = [0 | 1]
 - 0 indicates FastEthernet0/0
 - 1 indicates FastEthernet0/1

2. FE_SPEED_MODE = [0 | 1 |2 | 3 | 4]
- 0 indicates 10 Mbps, half-duplex
- 1 indicates 10 Mbps, full-duplex
 - 2 indicates 100 Mbps, half-duplex
 - 3 indicates 100 Mbps, full-duplex
 - 4 indicates Automatic selection (default)

For routers with Gigabit Ethernet interfaces, the following ROMmon variables should be available to indicate which Gigabit Ethernet port should be used, as well as the speed and duplex setting for that interface:

1. GE_PORT = [0 | 1 | 2]
- 0 indicates GigabitEthernet0/0
- 1 indicates GigabitEthernet0/1
- 2 indicates GigabitEthernet0/2

2. GE_SPEED_MODE = [0 | 1 |2 | 3 | 4 | 5]
- 0 indicates 10 Mbps, half-duplex
- 1 indicates 10 Mbps, full-duplex
- 2 indicates 100 Mbps, half-duplex
 - 3 indicates 100 Mbps, full-duplex
 - 4 indicates 1 Gbps, full-duplex
 - 5 indicates Automatic selection (default)
 
All user-defined ROMmon variable settings in the port properties must be the actual ROMmon variable name prepended with _rommon_. For example, to set the default gateway, configure the following property on the Local Manager port that is managing the router:

```
_rommon_DEFAULT_GATEWAY 192.0.2.254
```

Use the **config properties** command at the port level in the Local Manager to enter the port properties configuration editor.

```
[admin@UplogixLM (port1/4)]# config properties
[config properties]#
```

Once in the editor, you can use the ? command to view a list of possible configuration options.

```
[config properties]# ?
Allowable arguments are:
show
[propertyName] [propertyValue]
no [propertyName]
or 'exit' to save current values and quit config mode
[config properties]#
```
**show**

Display configured properties

**{no} {property name} {property value}**

Define property names. The no prefix will remove the property from the port.

Example: Instruct the Uplogix LM to transfer an image to the router, where auto negotiation should be used for interface GigiabitEthernet0/2, with an IP address of 192.0.2.142, a subnet of 255.255.255.0 and a default gateway of 192.0.2.254:

_rommon_IP_ADDRESS 192.0.2.142
_rommon_IP_SUBNET_MASK 255.255.255.0
_rommon_DEFAULT_GATEWAY 192.0.2.254
_rommon_GE_PORT 2
_rommon_GE_SPEED_MODE 5

**exit**

Exit the configuration editor.

# Display Properties

Use the **show properties** command to view the properties on the Local Manager port:

```
[admin@Uplogix (port1/4)]# show properties
_rommon_DEFAULT_GATEWAY: 192.0.2.254
_rommon_GE_PORT: 2
_rommon_GE_SPEED_MODE: 5
_rommon_IP_ADDRESS: 192.0.2.142
_rommon_IP_SUBNET_MASK: 255.255.255.0
```