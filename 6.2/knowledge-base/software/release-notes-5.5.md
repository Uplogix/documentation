<!-- 5.5 -->

Uplogix, Inc. is pleased to announce the release of version 5.5 software for the Uplogix Local Manager and the Uplogix Control Center.

The following software features, improvements, and fixes have been made in both the Local Manager and the Control Center software.

This document covers LMS version 5.5 and all subsequent patch releases. Changes made in patch releases are marked with the version number.

<div class='danger' />This software will not run on newer Local Managers, including the Uplogix LM80 and LM83X.</div>

<div class='warning' />This software will not run on EOL Local Managers, including the Uplogix 400, 430, and 3200. For more information, please contact Uplogix Support.</div>

# Uplogix Local Manager

## New Features and Improvements

### New Feature: IKEv2 VPN Support

IKEv2 addresses a number of shortcomings in IKEv1. The Local Manager utilizes certificates to authenticate to VPN servers like Cisco ASA, IOS, and pfSense/strongSwan.

### Improvement: Operating System

The operating system of the Local Manager has been rebuilt to use the latest embedded distribution technology.  The LMOS binary images are now 56MB, half the size of the previous release. The virtual Local Manager now includes open-vm-tools.

### Other Changes and Issues Addressed in This Release
 
* Made multiple Cisco driver speed and reliability improvements for pushing or pulling an OS or config.
* Added TLS 1.2 support with elliptical curve Diffie Hellman.
* TLS no longer supports traditional Diffie Hellman.
* FIPS mode no longer supports 3DES.
* The maximum length of the Local Manager hostname was increased from 22 to 63 characters.
* Updated APC driver to work with AOS v6.x.  Version '6' must be specified when initializing the port.
* Added new option to use DNS when provided by your PPP server.
* Local Manager no longer will get stuck on boot if Ethernet cable is accidentally plugged into console port.
* Improved automatic configuration of Verizon LTE modems.
* Improved support for large config and OS files on the Local Manager.
* Improved date consistency in 'Change' reports.
* Improved login responsiveness after a reboot.
* Addressed many Common Vulnerabilities and Exposures (CVEs). Consult the [CVE Database](https://uplogix.com/docs/cve) for more information.
* (**5.5.1**) Updated ServerTech Sentry driver to better support v8.0 of its CLI.
* (**5.5.1**) Security patch for "Zip Slip" vulnerability.
* (**5.5.1**) Fix to handle dropped connection to LM from Terminal application when forwarding ports.
* (**5.5.1**) Fix for "deny all" permission when used with IPv6.
* (**5.5.2**) Fix to handle SSH timeout during part of the handshaking process on slow networks when using some clients.
* (**5.5.3**) Added property to use reserved disk space to accommodate managed devices with very large operating system images.
* (**5.5.4**) Security patch for "SACK Panic" exploit (CVE-2019-11477).
* (**5.5.4**) Fix to allow import of full configuration XML file when LM is out of band.
* (**5.5.4**) Added support for Active Directory on Cisco ISE.
* (**5.5.4**) Added support for changing hostname and IP when LM is out of band. 

## Known Issues in This Release

* Version 5.5+ only supports the 500, 5000, and virtual Local Manager platforms.  Previous EOL models may continue to minimally heartbeat to the Control Center.

# Uplogix Control Center (UCC)

## New Features and Improvements

### **(5.5.1)** New Feature: Integration of Uplogix Terminal Windows application


* Some users may require this patch if using Java 11(+) since Java 11 drops support for JNLP.  Oracle ended public updates for Java 8 for commercial users on January 2019.  Some users  may choose to extend support of Java 8 by working with Oracle.
* Users can benefit from the Windows Installer as it decouples the Terminal application from requiring Java on the client's system.  The Uplogix Terminal application is a Windows installer that wraps the JNLP (applet) code as an installed Windows application that bundles Java with it.  This allows a user to continue running older versions of Java (e.g. 7) for legacy applications and also run the Uplogix Terminal application with the latest supported version of Java that Uplogix bundles with each release.
* By default, the 5.5.1 patch will continue to use JNLP and a user will not be required to make any changes.  The user  may also download the Windows Installer and use it with JNLP.  A user can change the default to UNLP for all users by editing embassy.overrides to include TERMINAL_LAUNCH=unlp.  This allows the Windows Terminal application to automatically associate and launch UNLP files without impacting any file association for JNLP the user may already have.
* Users can download the Windows Installer (MSI) from their profile page.
* The Windows Terminal application adds several benefits over default JNLP including status icons in the taskbar and a history of recent connections.
* The Windows Terminal application is also signed with an EV certificate so that users and Windows can trust the installer is safe.


### New Feature: IKEv2 VPN Support

IKEv2 can be configured from the Control Center.  Previously, server and CA certificates could only be managed in FIPS mode.  Now, they can be managed at the inventory group and Local Manager level regardless of FIPS mode to configure IKEv2 certificates for VPN servers.

### New Feature: Schedule 'Pull OS' and 'Pull Config'

Tasks 'pull os' and 'pull config' can now be scheduled from a port or a filter.

### Improvement: Better Monitoring and Debug Tools

The Control Center now shows a warning message under the 'Administration' tab if database backups have not run in the last 48 hours.  A warning message will also be shown if any disk partition exceeds 90% usage.  Anonymous usage statistics can now be easily collected and submitted to Uplogix under a new page called 'Support Tools'.  At this time, statistics are **not** automatically sent to Uplogix.  Report subscriptions can now be tested from the 'Support Tools' page as well.

### Other Changes and Issues Addressed in This Release

* Login banner now supports preformatted text.
* Login banner also supports replacement tokens for build information.
* Improved log management to prevent HA (standby) environments from filling the /usr partition.
* Added TLS 1.2 support with elliptical curve Diffie Hellman.
* Dial-in now supports ECDHE_RSA.
* Fixed a memory issue when running large reports.
* Improved performance of the heartbeat protocol.
* Improved performance of the 'Inventory' page.
* Added IPT SLV reports that can be run from the inventory or at a system level.
* Addressed many Common Vulnerabilities and Exposures (CVEs). Consult the [CVE Database](https://uplogix.com/docs/cve) for more information.
* **(5.5.1)** Security patches for the operating system.
* **(5.5.1)** Fix for "become-standby" bug that thought Tomcat was always running.
* **(5.5.1)** Fix for 5.5.0 bug where SSH applet application would break if compression was enabled.
* **(5.5.2)** Security patches for the operating system (bind, kernel, ntp, yum).
* **(5.5.2)** Fix for French keyboard tilde (and other dead keys) being recognized by the Uplogix Terminal application.
* **(5.5.2)** Fix for timeout issue with Cisco 890 series routers used as modem access server.
* **(5.5.3)** Fix for ZombieLoad exploit (CVE-2018-12130).
* **(5.5.4)** Added support for SOCKS proxy (SS5) in the Uplogix Terminal Windows application.  
* **(5.5.4)** Patched OS (kernel, bind, python, SACK Panic).

## Known Issues in This Release

* Java applications launched from IE 11 on Windows 10 require 32-bit Java.  This affects all Java applications including the Uplogix SSH and Dial-in applications.  Oracle released an article about this issue https://java.com/en/download/faq/java_win64bit.xml.


# Release Dates and Build Numbers


## Version 5.5.0
* Release Date: 5/7/2018
* Build Number: 32896

## Version 5.5.1
* Release Date: 2/15/2019
* Build Number: 34099

## Version 5.5.2
* Release Date: 3/27/2019
* Build Number: 34294

## Version 5.5.3
* Release Date: 5/31/2019
* Build Number: 34684

## Version 5.5.4
* Release Date: 7/3/2019
* Build Number: 34881