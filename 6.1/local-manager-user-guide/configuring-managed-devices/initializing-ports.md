# Overview
The Local Manager uses the default serial settings of 9600, 8, n, 1 when operating in native mode.

When connecting a device, the next step is to initialize the Local Manager port to use the appropriate driver and to enable active monitoring and control of the managed device. Uplogix recommends logging into the device to verify serial communication settings and passwords prior to port initialization. Then navigate to the appropriate port resource and use the **config init** command to set up the port. This must be performed even if the native settings are appropriate for the device; otherwise, the device information is not displayed when using the **show dashboard** command.

The settings presented vary by device make and model. Refer to the deviceâ€™s documentation for configuration settings. In addition, Ethernet-related settings are not presented if the Local Manager does not have dedicated device Ethernet ports.

```
[admin@UplogixLM (port1/1)]# config init
--- Enter New Values ---
description: AUS-CORE Primary Cisco Router
make [native]: cisco
model: 
os: IOS
os version: 
management IP: 
Configure dedicated Ethernet port? (y/n) [n]: n
console username: 
console password: ****
confirm password: ****
enable username: 
enable password: *****
confirm password: *****
secondary console username: 
secondary console password: 
secondary enable username: 
secondary enable password: 
Serial Bit Rate [9600]: 
Serial Data Bit [8]: 
Serial Parity [none]: 
Serial Stop Bit [1]: 
Serial Flow Control [none]: 
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
Retrieving device information directly from device...
Hostname     : AUS-CORE
Serial Number: JAD06100H16
Make         : cisco
Model        : 2610
OS Type      : IOS
OS Version   : 12.2(26)
Uptime       : 18 hours, 26 minutes
System image file is "flash:/c2600-i-mz.122-26.bin"
Updating model.
Updating OS version.
Initialize device logging
Scheduling default jobs
Testing job deviceInfo
Hostname     : AUS-CORE
Serial Number: JAD06100H16
Make         : cisco
Model        : 2610
OS Type      : IOS
OS Version   : 12.2(26)
Uptime       : 18 hours, 27 minutes
System image file is "flash:/c2600-i-mz.122-26.bin"
Job deviceInfo was successful
Job deviceInfo was scheduled
Testing job rulesMonitor
Job rulesMonitor was successful
Job rulesMonitor was scheduled
Testing job pullRunningConfig
Retrieving running-config from device ...
Failed to transfer 'running-config' via TFTP
Could not retrieve running-config.
Unable to retrieve configuration via network.
Attempting to retrieve configuration using the console...
Complete. running-config pulled.
running-config saved to archive as current.
Job pullRunningConfig was successful
Job pullRunningConfig was scheduled
Testing job pullStartupConfig
Retrieving startup-config from device ...
Failed to transfer 'startup-config' via TFTP
Could not retrieve startup-config.
Unable to retrieve configuration via network.
Attempting to retrieve configuration using the console...
Complete. startup-config pulled.
startup-config saved to archive as current.
Job pullStartupConfig was successful
Job pullStartupConfig was scheduled
Testing job pullVlanConfig
Retrieving vlan.dat from device...
Finding vlan.dat on device...
No vlan.dat file present.
Job pullVlanConfig was successful
Job pullVlanConfig was scheduled
Testing job pullOS
Starting pull of Cisco IOS Image
System image file is "flash:/c2600-i-mz.122-26.bin"
Backing up OS file: flash:c2600-i-mz.122-26.bin
- Output removed -
```

**Description** (optional free text field up to 255 characters) â€“ Optionally, enter information about the device attached to the port. If left blank, the device hostname will automatically be used. This field will be displayed as part of the information that normally scrolls on the Local Manager front panel display.

> Some symbol characters, such as the ~ and \ are not shown correctly on the front panel display.

**Make** (required) â€“ The available settings for make are: 

```
 3Com
 Alcatel
 APC
 Avocent
 BayTech
 Brocade
 Cisco
 Comtech
 enhanced
 Foundry
 Garmin
 GE
 Gilat
 HP
 IBM
 iDirect
 Juniper
 Lantronix
 MRV
 native
 ND SatCom
 Netscreen
 Nortel
 PPP
 SeaTel
 server
 ServerTech
 SpaceTrack
 Sun
 Tasman
 Tippingpoint
 TracStar
```
 
Use the native setting for devices that are not explicitly supported.

See the [Configuration Guides](http://uplogix.com/docs/local-manager-user-guide/configuration-guides) section for detailed configuration information for supported devices.

**Model** (automatic free text field of up to 255 characters) â€” Information entered in this field is replaced by what the Local Manager detects on this port, unless the device is configured as native.

**Operating system** (required) â€” Available settings depend on the specified make. For example, BayRS for Nortel; IOS/IOS-XE, NX-OS, ASA, Pix or CatOS for Cisco; JunOS for Juniper; TOS for TippingPoint; and TiOS for Tasman.

Enter a question mark to view the available options. For example, after choosing "Cisco" as a make:

```
os: ?
'?' is not supported.
Please choose from one of the following values:
 ASA
 CatOS
 IOS
 NX-OS
 Pix
 ```

**Operating system version** (automatic free text field of up to 255 characters) â€” Information entered in this field is replaced by what the Local Manager detects on this port, unless the device is configured as native.

**Management IP address** (optional) â€” This field is for the management IP address of the managed device.  For the case of a Cisco router, it is best to use the lowest numbered interface on the router (GigabitEthernet0/0, for example), as this address and interface are used by default with the TFTPDNLD functionality during ROMmon recovery and when sourcing SNMP traps sent on behalf of the device.

**Dedicated Ethernet port** (optional) â€” The dedicated Ethernet port is used to create a reliable, direct Ethernet connection between the Local Manager and the managed device. If configured, the Local Manager will use this connection to move OS and configuration files back and forth between the managed device and the Local Manager using such file transfer protocols like FTP, SFTP/SCP and TFTP. If the port is configured, a non-overlapping IP subnet must be used for the dedicated link. Non-routable private (RFC 1918) addresses such as 169.254.x.x are recommended. To configure a dedicated Ethernet port, enter **y**.

**Use DHCP** (available if you opt to configure a dedicated Ethernet port) â€” Configures the Local Manager to provide the managed device dedicated Ethernet interface with an IP address via DHCP. When using DHCP, be sure to configure the managed device dedicated Ethernet port to use DHCP to get its IP address.

>To use this feature, you must also configure the Local Manager to assign DHCP addresses. Refer to Configuring the Local Manager to assign DHCP addresses to connected devices.

**Dedicated device IP** (required if using static addressing for the dedicated Ethernet port) â€” The IP address on the managed device. This IP address is not used in SYSLOG/SNMP messages for this device, but can be used in device recovery to communicate directly to the managed device and move files.

**Dedicated port IP** (required if using dedicated Ethernet port) â€” The dedicated Ethernet link IP address for the Local Manager.

**Dedicated Ethernet subnet mask** (required if using dedicated Ethernet port) â€” The subnet mask for the dedicated Ethernet link. Since this is a point-to-point Ethernet connection all that is required is a 255.255.255.252 mask.

> The dedicated network of each device must be on its own IP subnet.

**Port speed** (optional) â€” The speed used by the deviceâ€™s Ethernet port. Speed can be set for better performance or to overcome auto-negotiation problems. Available settings are 10half, 10full, 100half, 100full, 1000full and auto (default).

**Console username** (optional free text field) â€” Enter the username to be used to access the managed device for the case where a username is required to access the device.

**Console password** (optional free text field, usually required) â€” Enter the password to be used to access the managed device for the case where a username/password or just a password is required to access the device.

**Enable username** (optional free text field) â€” If there is no privileged super user account this field is not necessary. Leave this field blank for the case where there is only an enable password to enter privileged mode.

**Enable password** (optional free text field, usually required) â€” This password is used to enter privileged mode on a Cisco device or as the root password for Juniper devices.

**Secondary Console username** (optional free text field) â€” For use in situations that require the device to utilize an alternate authentication scheme â€“ for example, you may want to failover to using a locally defined user account when AAA servers are unreachable.

**Secondary Console password** (optional free text field) â€” For use in situations that require the device to utilize an alternate authentication scheme â€“ for example, you may want to failover to using a locally defined user account when AAA servers are unreachable.

**Secondary Enable username** (optional free text field) â€” For use in situations that require the device to utilize an alternate authentication scheme.  Leave this field blank for the case where there is only an enable password to enter privileged mode.

**Secondary Enable password** (ptional free text field) â€” For use in situations that require the device to utilize an alternate authentication scheme. This is usually the same enable password as is used for the other/primary login credentials.

**Serial bit rate** (optional) â€” The bit rate used by the managed device. Available settings are 1200, 2400, 4800, 9600, 19200, 38400, 57600, and 115200.

**Serial data bit** (optional) â€” The number of data bits (7 or 8) used by the managed device. 

**Serial parity** (optional) â€” The parity setting (none, even, or odd) used by the managed device.

**Serial stop bit (**optional) â€” The number of stop bits (1 or 2) used by the managed device. 

**Null modem** (400 and 3200 Local Manager onlyâ€” optional) â€” If a rolled cable is used, enter y.

**Commit changes** (required) â€” You must commit changes before they are implemented.

When changes are committed, the Local Manager queries the device based on the information entered. Model and OS version may be replaced with specific information collected from the device. 