<!-- 5.4 -->
<div class='ucc' />Administration > Server Settings</div>

Server settings can be accessed from the Administration tab on the main navigation bar. It is the default view presented when the Administration link is clicked.

![Uplogix Control Center Administration Server Settings](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-administration-server-settings.png)

Once settings have been changed, click **Save** in the upper right or lower right to save the new settings.

# Install Information

This section provides the following information:

* IP - IP address of the Control Center
* Hostname - Hostname of the Control Center
* Version - Currently installed software version
* Build ID - Denotes the build ID of the currently installed software version (there can be multiple version of 5.5 before a final *generally available* version is released.)
* Install Date - When the software was installed
* Standby Status - Denotes the status of High Availability Control Centers
	* not configured
	* unknown/out of data
	* out of sync
	* in sync
* License Support - Lists the number of systems and virtual ports allowed by the currently installed license.
* (**v5.5.1** or later) Terminal Launch - Denotes file type used for [Uplogix Terminal App](https://uplogix.com/docs/control-center-user-guide/applet/terminal-app "Uplogix Terminal App") 

# Basic Settings
## Login Banner

Specify the text to display in the Control Center login screen. Line breaks entered in this text box are ignored. 

Use only printing characters in the banner and other text fields. Spaces are considered printing characters.

## Session Timeout

By default, Control Center sessions time out after 30 minutes of inactivity. If this does not meet your organization's needs, change the value for Session timeout. You can set the timeout to any integer value from 5 to 1440 minutes (24 hours).

Once finished making changes, click **Save**.

The session timeout for Local Managers is set separately. 

> If your session times out, you will be logged out but any operation in progress will not be affected. When you log in again, you are returned to the same page.

## Time Zone

<div class='danger'>Correct Control Center time is critical and should be provided by an NTP server. </div>

Setting the time zone does not change the system time of the Control Center. This setting is only used for display purposes. The Uplogix Control Center should always be set to UTC time.

## Use DST

Select *Use DST* to adjust Daylight Saving time in reporting.

# Mail Settings

See *[Configuring Mail Settings](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/mail-settings)*.

# Reverse SSH Tunnel Settings

See *[Configuring Reverse SSH Tunnels](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/reverse-ssh-tunnels)*.

# SNMP Settings

The Control Center can be configured to send SNMP traps to an SNMP manager. Traps collected from Local Managers will be sourced with the Local Manager's IP address.

SNMP MIB definitions are available under /home/emsadmin/ on the Control Center.

```
[emsadmin@UplogixControlCenter ~]$ less uplogix-mib.txt 
--
--  Uplogix Enterprise Specific MIB: Chassis MIB
--
-- Copyright (c) 2016 Uplogix, Inc.
-- All rights reserved.
--
-- The contents of this document are subject to change without notice.
--
-- Generated: 2016-01-28T22:09:33-06:00

        UPLOGIX-SMI DEFINITIONS ::= BEGIN
 
                IMPORTS
                        NOTIFICATION-GROUP
                                FROM SNMPv2-CONF
                        OBJECT-TYPE, MODULE-IDENTITY,
                        OBJECT-IDENTITY, NOTIFICATION-TYPE, enterprises
                                FROM SNMPv2-SMI
                        DisplayString
                                FROM SNMPv2-TC;
```

