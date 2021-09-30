<!-- 5.4 -->

Interactive command that steps you through the initial configuration necessary for the Uplogix Local Manager to communicate with the network device. If you are configuring a server, you may also wish to configure its service processor using the **config service-processor** command.

# Command availability 

CLI resource: port, modem

Device makes: All

Modem : All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config init
```

# Settings 

The following settings are presented for the port resource.

Ethernet-dependent settings are not available from the Uplogix 430 Local Manager.

**description** (optional) - Used to identify the device if no hostname is found. The first word of the description will be used as the device's hostname, and will be displayed on the front panel as it scrolls information.

> **Note**: Some symbol characters, such as the ~ and \ characters, are not shown correctly on the front panel display.

**make** (required) - Type ? to see a list of supported devices. If your device is not listed, enter native.

**model** (optional) - Automatically discovered during assimilation of supported devices.

**os** (required in most cases) - Type **?** to see a list of supported OS types. This list is filtered based on the make.

**os version** (optional) - Automatically discovered during assimilation of supported devices.

**management IP** - Required if Ethernet-based functionality is desired. This is the regular IP address of the device and not related to the dedicated Ethernet between the Uplogix Local Manager and the device.

**configure dedicated Ethernet port?** - Required if dedicated Ethernet functionality is desired. This network must be unique across all device ports on the Local Manager. 

> **Note**: If you configure a dedicated Ethernet port on a switch, set the switch to use DHCP or configure the STP portfast feature on the layer 2 interface to improve performance.

**Use DHCP?** - Specifies whether the device requests a DHCP address from the Local Manager series Local Manager. This command is presented only if you choose to configure a dedicated Ethernet port. 

> **Note**: If you configure the device to use DHCP, ensure that the Local Manager is configured to serve DHCP addresses to managed devices. Use the config system protocols DHCP command to do change the default of 169.254.100.

**dedicated device IP** (optional) - IP address of the device's Ethernet interface.

**dedicated port IP** (optional) - IP address of the port's Ethernet interface.

**dedicated netmask** (optional) - Subnet mask for the dedicated Ethernet. Each port must be on its own subnet.

**speed/duplex** (optional) - Defaults to auto but can be changed to suit your network.

**console username** - Depends on the login process of the device. 

**console password** - Depends on the login process of the device. 

**enable username** - Depends on the enable process of the device. 

**enable password** - Depends on the enable process of the device. 

**Secondary Console username** (Cisco only - optional free text field) 

**Secondary Console password** (Cisco only - optional free text field)

**Secondary Enable username** (Cisco only - optional free text field)

**Secondary Enable password** (Cisco only - optional free text field) 

**serial bit rate** (optional) - Defaults to 9600.

**serial data bit** (optional) - Defaults to 8.

**serial parity** (optional) - Defaults to none.

**serial stop bit** (optional) - Defaults to 1.

**serial flow control** (optional) - Defaults to none.

The settings that are presented depend on the resource and the specific device. 

Typical setting prompts for the modem resource:

```
description: []:
make: [embedded]:
serial bit rate [38400]:
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
serial flow control [none]:
```

Typical setting prompts for a port device that you have specified as a Cisco product using CatOS:

```
description:
make [native]: cisco
model:
os: ios
os version:
management IP:
console username: cisco
console password: *****
confirm password: *****
enable username:
enable password:
secondary console username:
secondary console password:
secondary enable username:
secondary enable password:
Serial Bit Rate [9600]:
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:

```

# Usage 

```
[admin@UplogixLM (port1/1)]# config init
--- Enter New Values ---
description: tasman6300
make [native]: tasman
model: 6300
os: tios
os version:
management IP:
console username: tasman
console password: ********
confirm password: ********
enable username:
enable password:
Serial Bit Rate [9600]:
Serial Data Bit [8]:
Serial Parity [none]:
Serial Stop Bit [1]:
Serial Flow Control [none]:
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
Retrieving device information directly from device...
Hostname     : TASMAN-6300
Serial Number: 63000AISD0510009
Make         : tasman
Model        : 6300
OS Type      : TiOS
OS Version   : r6
Uptime       : 121:11:35
Updating OS version.
Assimilating the device will set buffered logging on the console.
Proceed? (y/n): y
Retrieving running-config from device via console...
Done.
```

# History 

1.06 - Ethernet Link negotiation was added.

2.5 - Command now available on modem resource.

3.2 - Changed make generic to native. Added secondary console and enable credentials for Cisco devices.

3.4 - Added the ability to allow the device to receive a DHCP address from the Local Manager.

# Related commands 

- **config info**
- **config authentication**
- **config serial**
- **config outlets**


