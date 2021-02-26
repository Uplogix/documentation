# Overview

Uplogix, Inc. is pleased to announce the release of version 6.0 software for the 500 and 5000 models of the Uplogix Local Manager (LM) and Uplogix Control Center (UCC).

The following software features, improvements, and fixes have been made in both the Local Manager and the Control Center software.

This document covers LMS version 6.0 and all subsequent patch sub-releases. Changes made in patch releases are marked with the version number.

# Uplogix Local Manager Updates

## New Features and Improvements

### New Feature: Added config apn command to modem resource

Users are now able to configure cellular modem APN information from within the Local Manager CLI itself. If the Local Manager is managed by a UCC, its APN information can be configured there as well.

### Improvement: Optimized Available Storage Space

Supports an increased number of larger device operating system files for storage on managed device ports.

### Improvement: Advanced Cisco IOS/IOS-XE Driver

Enhanced reliability to detect and recover from corrupted or missing configuration files, as well as upgrading and downgrading running OS releases, when an advanced driver is initialized against a device that has an OS file which has been stored on the Local Manager. 

### Improvement: Additional LTE Modems

LTE modem module support has been increased to include Sprint (Category1), Verizon/AT&T Combo (CategoryM1) and Verizon/AT&T Combo (Category4). These newly added modems enjoy the same full functional support as existing units.

### (6.0.1) Improvement: Push OS command better supports IOS-XE stacked switches running in bundled mode

An OS image can be pushed to the master switch in a booted and operational Cisco switch stack. All members of the stack will receive the image and will be configured to boot from it. If configured, the entire stack will be rebooted automatically. Otherwise, the stack will need to be rebooted manually.

## Other Changes and Issues Addressed in This Release

* LCD panel now correctly notes â€œLOCKED BY OOBâ€ when a Local Manager is actively using PPP for its own management connectivity.
* Addressed SACK panic issue. Local Managers no longer accept packets which try to force an MSS > 512.
* Enhanced Virtual Local Manager performance on KVM by configuring a virtual hardware RNG device.
* Several SSH vulnerabilities and exploits were addressed.
* Running **config init** against a supported power controller will display the actual port names, as defined by the manufacturer.
* If an LTE modem becomes unresponsive, a reset of the modem will be executed.
* Fixed an issue where decompression of ZIP files could lose track of, and fail to verify, destination directories.
* Fixed an issue where configuring an IP protocol filter with a *deny all* entry would work incorrectly with IPv6.
* Fixed issue where issuing a **config system route** while outband was active could result in a network â€œbounceâ€ and spoilage of an active PPP session.
* Improved the booting reliability and predictability of Uplogix 500 Local Managers.
* Fixed an issue where configuration import and export would silently fail when outband was active.
* Fixed an issue where dedicated Ethernet port MAC addresses would be incorrectly defined.
* Fixed an issue where traffic from a subinterface on given layer 3 network destined for other subinterfaces on the same layer 3 network, or bond0, did not return correctly.
* Fixed an issue where removing and then inserting into a USB port required up to 60 seconds between events. Wait time is now significantly less than 1 second.
* Local Managers now support custom port numbers for SCP, FTP, HTTP with all file transfer commands.
* Cleaned up and enhanced the general display of information pulled from managed power controllers.
* The <span class='font-weight-bold'>show session * | grep</span> command no longer hangs when parsing very large amounts of text (i.e., no longer results in possibly hundreds of screens of text)
* Added SSH Key Exchange options of â€œECDHâ€ and â€œECDH+GCMâ€ to SSH configuration parameters.
* Failures arising as a result of the use of command **outband cycle heartbeat** now contain a more robust set of diagnostic information.
* Improved the **show buffer** commandâ€™s handling of non-ASCII characters.
* Enhanced readability and helpfulness of SCP server setup help text.
* VPN no longer attempts to connect indefinitely if there is an existing tunnel. It will now cease trying gracefully.
* Improved the login prompt regex parsing for the Enhanced driver.
* **config update http** command now supports sites requiring HTTPS access.
* Enhanced speed and responsiveness of screen paging when text results exist over multiple screens.
* Enhanced our SCP support to refuse multiple files being maliciously sent when only a single file was requested.
* Cleaned up front panel LCD display regarding IPv6 address readouts.
* Improved system reporting on dedicated Ethernet cards in the event of a port or entire card failure.
* Refined system error messages for Cisco NX-OS devices when attempting to execute push os.
* Addressed the following Common Vulnerabilities and Exposures (CVEs):
 * CVE-2019-11815
 * CVE-2019-11477, CVE-2019-11478, CVE-2019-11479
* (6.0.1) Improved serial communication stability for NetApp Filers operating at 115200 baud.
* (6.0.1) Improved stability of IKEv1 VPN connections over out-of-band channels.
* (6.0.2) Corrected "modem unavailable" error for v92 modems with missing product/vendor IDs
* (6.0.2) Removed support for 1024-bit DSA SSH host keys

# Uplogix Control Center (UCC) Updates

## New Features and Improvements

### New Feature: Announcement Banner

On the Administration screen, an Announcement Banner option has been added. Any information added in the associated field will be prominently displayed at the top of every Control Center page for every user who logs on. This is an easy way to promote important notices to all UCC users who log into the associated Control Center.

### Improvement: Control Center Terminal Application

The Uplogix Terminal Application enables access to the Local Manager through a Java Runtime Environment which is now entirely enclosed and thus no longer requires users to separately install and maintain Java environments on client systems. Older JNLP files have been eliminated and replaced with UNLP files.
Additionally, the Terminal Application no longer requires a browser and is now a certified Windows application. 

There are several options for running the Terminal Application in locked-down environments, and the Terminal Application can delegate to the client system for Java or use JNLP as a legacy option.

### Improvement: Comprehensive GUI Rework

Two primary aspects were addressed: overall look-and-feel and functional improvements regarding search filters. The visual aspects and layouts of web pages have been made more consistent and context-aware regarding placement of input fields, margins, etc. The search filter pages have more reasonable default sort states, more consistently context-aware menus, and improved visibility of warnings and other notices.

### Improvement: Graphical Display of Local Manager Provisioning

On a given Local Managerâ€™s summary page, the graphical representation of the way it is provisioned with regards to expansion and transport modules is now accurately displayed. The static model image displayed in previous releases has been removed.

## Other Changes and Issues Addressed in This Release

* Corrected an issue where a standby UCCâ€™s database can become â€œout-of-sync" as the result of a 100% loaded CPU, causing the associated recovery script to become â€œstuckâ€, necessitating a restart of the database.
* Improved the ability of the Dashboard screen to handle very large amounts of entries (thousands).
* Strengthened support of SOCKS5 proxy in the Terminal Application.
* Content-Security-Policy and Referrer-Policy have been fully implemented.
* â€œDownloadâ€ button is no longer actionable when there are no inventory session logs to download.
* Added a â€œCreate Filterâ€ button on the Deployment Overview page.  The resulting filter can be used to easily schedule upgrades against a specific Uplogix version regardless of Inventory group association.
* Added a report to display the IMEI number for each managed modem, sorted by Local Manager name and then Serial number.
* On the Network Protocols Settings page, protocols which are considered less secure and risky, but which might be nonetheless needed due to legacy requirements, are more clearly displayed.
* Enhanced the flexibility and consistency of the Terminal Application when connecting to a broader array of third-party device modems.
* Addressed and resolved an Uplogix Terminal Application connectivity issue involving one-time-use passwords.
* Improved the handling of Control Center window size adjustments to more effectively display large amounts of information.
* A general email alert message can now be easily configured to be sent to all active users.
* Addressed the relevant following Common Vulnerabilities and Exposures (CVEs):
 * CVE-2018-12126/12127/12130/11091: The â€œZombieLoadâ€ issue.
 * CVE-2018-8014
 * CVE-2019-17055
 * CVE-2019-17133
 * CVE-2020-5208
 * CVE-2017-15670/CVE-2017-15804
 * CVE-2018-12020
 * CVE-2018-3639
 * CVE-2019-3855/CVE-2019-3856/CVE-2019-3857
 * CVE-2019-3863
 * CVE-2018-12384
 * CVE-2018-15473
 * CVE-2019-10160
 * CVE-2019-9636
 * CVE-2018-1124/CVE-2018-1126
 * (6.0.1) CVE-2020-8616
 * (6.0.1) CVE-2020-8617
 * (6.0.1) CVE-2020-0543
 * (6.0.1) CVE-2020-10711
 * (6.0.1) CVE-2017-12192
 * (6.0.1) CVE-2019-17666
 * (6.0.2) CVE-2017-2647
	
# Release Dates and Build Numbers

Version 6.0.0
* Release Date: 5 May 2020
* Build Number: 35905

Version 6.0.1
* Release Date: 24 July 2020
* Build Number: 36252

Version 6.0.2
* Release Date: 25 September 2020
* Build Number: 36661