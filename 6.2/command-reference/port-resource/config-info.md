<!-- 5.4 -->

Interactive command that steps you through the changes needed to update the Uplogix Local Manager's settings used to communicate with the network device. 

# Command availability
 
CLI resource: port, powercontrol, modem

Device makes: All

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config info
```

# Usage 

The configuration choices presented depend on the device and on the model of Local Manager you are using. Dedicated Ethernet options require a dedicated Ethernet module.

If no hostname is available, first word of the description will be used as the device's hostname, and will be displayed on the front panel and Dashboard.

> **Note**: Some symbol characters, such as the ~ and \ characters, may not display correctly on the front panel display.

```
[admin@UplogixLM (port1/1)]# config info
Hostname:
Description: tasman6300
Make: tasman
Model: 6300
OS: tios
OS Version:
Management IP:
DHCP Enabled: true
Dedicated Device IP: 169.254.100.2
Dedicated Port IP: 169.254.100.1
Dedicated Subnet: 255.255.255.252
Dedicated Speed/Duplex: auto:100full
Change these? (y/n) [n]: y
--- Enter New Values ---
description: [tasman6300]:
make: [tasman]:
model: [6300]:
os: [tios]:
os version: []:
management IP: []:
configure dedicated ethernet port? (y/n) [n]: y
Use DHCP? (y/n) [y]: n
dedicated device IP [169.254.100.2]:
dedicated port IP [169.254.100.1]:
dedicated netmask: [255.255.255.252]:
speed/duplex: [auto]:
Do you want to commit these changes? (y/n):

```

**description** (optional) - Used to identify the device if no hostname is found.

**make** (required) - Type ? to see a list of supported devices. If your device is not listed, enter native.

**model** (optional) - Automatically discovered during assimilation of supported devices.


**os** (required in most cases) - Type ? to see a list of supported OS types. This list is filtered based on the make.

**os version** (optional) - Automatically discovered during assimilation of supported devices.

**management IP** - Required if Ethernet-based functionality is desired. This is the regular IP address of the device and not related to the dedicated Ethernet between the Uplogix Local Manager and the device.

**configure dedicated Ethernet port?** - Required if dedicated Ethernet functionality is desired. This network must be unique across all device ports on the Local Manager.

> **Note**: If you configure a dedicated Ethernet port on a switch, set the switch to use DHCP or configure the STP portfast feature on the layer 2 interface to improve performance.

**Use DHCP?** - Specifies whether the device requests a DHCP address from the Local Manager series Local Manager. This command is presented only if a dedicated Ethernet port is installed. 

> **Note**: If you configure the device to use DHCP, ensure that the Local Manager is configured to serve DHCP addresses to managed devices. Use the config system protocols DHCP command to change the default (169.254.100.x).

**dedicated device IP** (required) - IP address of the device's Ethernet interface.

**dedicated port IP** (required) - IP address of the port's Ethernet interface.

**dedicated netmask** (required) - Subnet mask for the dedicated Ethernet. Each port must be on its own subnet.

**speed/duplex** (optional) - Defaults to auto but can be changed to suit your network.

# History 

1.06 - Ethernet Link negotiation was added.

2.5 - Command now available on modem resource.

3.2 - Changed make "Generic" to "Native".

3.4 - Added "Use DHCP?" prompt.

# Related commands 

- **config init**
- **show info**
