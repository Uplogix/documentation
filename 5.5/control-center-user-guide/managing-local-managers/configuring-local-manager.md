<!-- 5.4 -->
<div class='ucc' />Inventory > Local Manager Summary page</div>

The Control Center provides a graphical interface for the configuration of managed Local Managers. Use the configuration menus on the left side of the Summary page to view and edit settings. The configuration menus cover most but not all of the features found on the LM command line.

![Uplogix Control Center - Local Manager Summary - Configuration](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-local-manager-summary-configuration.png)

Click on the right arrow on the configuration menu to expand it.

> Use only printing characters when completing text fields. Spaces are considered printing characters.

To change the Local Manager's configuration, select an option from the menu on the left. Enter the updated values and click **Save** to force the changes onto the Local Manager.

Some options may be unavailable, depending on your privileges. The IPT option is available only if the Local Manager has a [Service Level Verification (SLV)](http://uplogix.com/docs/local-manager-user-guide/advanced-features/service-level-verification) license.

# Configuration Menus

## Automation

### IPT

Required permission: **config system ipt**

Configure the Local Manager's SLV Voice Testing service. 

### OS Policies

Manage operating system standard policies per make and model for the deployment.

See [Operating System Policies](http://uplogix.com/docs/control-center-user-guide/managing-local-managers/os-policies)

### Rules

Required permission: **config rules**

Create and update rules on the Local Manager.

See [Rules and Monitors](http://uplogix.com/docs/control-center-user-guide/managing-local-managers/rules-and-monitors)

### Rule Sets

Required permission: **config ruleset**

Create and update rule sets on the Local Manager.

See [Rules and Monitors](http://uplogix.com/docs/control-center-user-guide/managing-local-managers/rules-and-monitors)

### SLV Tests

Required permission: **config slv**

Configure and view SLV tests. 

**SLV license required.**

## Network

### DNS

Required permission: **config system ip**

Configure DNS settings.

*Automatic configuration available via [Zero Touch Deployment](http://uplogix.com/docs/local-manager-user-guide/system-configuration/zero-touch-deployment)*

### IP

Required permission: **config system ip**

Configure IP settings or enable DHCP for automatic configuration.

*Automatic configuration available via [Zero Touch Deployment](http://uplogix.com/docs/local-manager-user-guide/system-configuration/zero-touch-deployment)*

### IPv6

Required permission: **config system ipv6**

Configure IPv6 settings or enable autoconf for automatic configuration.

### Management Server

Required permission: **config system management**

Enable Control Center management for a Local Manager and configure Heartbeat settings.

*Automatic configuration available via [Zero Touch Deployment](http://uplogix.com/docs/local-manager-user-guide/system-configuration/zero-touch-deployment)*

### NTP

Required permission: **config system ntp**

Specify NTP server(s) for time synchronization.

*Automatic configuration available via [Zero Touch Deployment](http://support.uplogix.com/hc/en-us/articles/204810359)*

### Protocols

Required permissions: **config system protocols filter**, **config system protocols ssh**, **config system protocols telnet**

Configure SSH, Telnet, IP filtering, and internal DHCP server settings.

Configure pass-through settings for SSH and Telnet.

### Proxy

Required permissions: **show system applet**

Configure settings for SOCKS Proxy used by CLI and DIAL applets.

### Reverse SHH

Required permissions: **show system reverse-ssh**

Configure settings for Reverse SSH Tunnel service.

See [Reverse SSH Tunnels](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/reverse-ssh-tunnels)

### Secondary Ethernet

Required permissions: **config system secondary**

Configure the Local Manager's secondary ethernet settings.

### SNMP

Required permissions: **config system snmp**

Enable and configure the Local Manager to respond to SNMP requests. Supports SNMP V3 only.

### Syslog

Required permissions: **config system syslog-options**

Configure the Local Manager to send data to a syslog server.

### Subinterfaces

Required permissions: **config system subinterface**

Configure and view subinterfaces defined on the Local Manager.

## Out-of-Band

### Setup Wizard

The Out-of-Band Setup Wizard will step you through the most common configuration options. Configures modem, dial-in, dial-out, Pulse, and VPN settings.

### Modem

Required permissions: **config answer** on modem resource

Configure answer settings, init string, and CallerID filtering.

### PPP

Required permissions: **config ppp** on modem resource

Configure dial-up information for establishing out-of-band connections. Enable Out-of-Band Sharing.

### Pulse

Required permissions: **config system pulse**

Configure Pulse settings, including Pulse Server IPs and automatic Out-of-Band.

### VPN

Required permissions: **config vpn** on modem resource

Configure VPN type and related settings.

## Security

### Authentication

Required permissions: **config system authentication**

Configure authentication settings, including TACACS, RADIUS, and Local authentication.

### Passwords

Required permissions: **config system authentication**

Configure password requirements.

### Privileges

Required permissions: **config privileges**

Configure user permissions for local resources.

### Roles

Required permissions: **config rules**

Create or update rules on the Local Manager.

## System

### Archive

Required permissions: **config system archive**

Configure archiving frequency for offloading Local Manager data to the Control Center.

### Banners

Required permissions: **config system banner**

Set login and welcome banners.

### Default Port Settings

Required permissions: **config settings**

Edit or delete default port settings.

### Email

Required permissions: **config system email**

Configure email settings for Local Manager alerting.

### Environment

Required permissions: **config system environment**

Configure temperature and humidity thresholds. Enable alarms for power supply and Ethernet link failures.

### Export

Required permissions: **config system export**

Configure settings for data export.

### LCD

Required permissions: **config system keypad**

Lock the front keypad and disable information display on the LCD.

### Properties

Required permissions: **config system properties**

Configure key/pair properties on the Local Manager.

### Serial

Required permissions: **config system serial**

Specify whether the Local Manager should use DCE or DTE for its serial management port.

### Timeout

Required permissions: **config system timeout**

Set the idle timer for CLI sessions. Separate from terminal pass-through idle timer.

### Virtual Slots

Required permissions: **config system slot**

Configure or remove virtual slots. 

# Group-level configuration

Configuration settings are also available on the Inventory Group level. However, some Local Manager-specific settings such as IP address cannot be applied to an inventory group.