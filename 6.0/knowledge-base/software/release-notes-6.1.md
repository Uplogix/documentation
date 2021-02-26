# Overview 
Uplogix, Inc. is pleased to announce the release of version 6.1 software for the Uplogix Local Manager and for the Uplogix Control Center.

The following software features, improvements and fixes have been made in both the Local Manager and the Control Center software.

This document covers LMS version 6.1 and all subsequent patch sub-releases. Changes made in patch releases are marked with the version number.

# Requirements
* LMS 6.1 is supported on Uplogix 500, 5000, LM80, LM83X, and Virtual Local Managers. Previous hardware platforms are not supported.
* LMS 6.1 supports upgrades from version 5.5.x and 6.0.x.
* LMS 6.1 is **not** supported on Control Centers running on Dell 2850, 2950, or R710 servers.

# CentOS 8
The operating system of the Uplogix Control Center has been upgraded from CentOS 6 to CentOS 8. 

## Important Changes

* Only TLS 1.2 and above are supported. A Control Center will not communicate with Local Managers running versions 5.4 and below, **even in minimal heartbeat**.
* SMTP certificates may need to be reconfigured after migrating to CentOS 8.
* FreeRADIUS configurations may need to be redone after migrating to CentOS 8.

## Usage Notes

* With the exception of Uplogix services (tomcat, migration, matchmatcher, ss5), **systemctl** has replaced the **service** command. Instead of **service network restart**, run **systemctl restart NetworkManager**.
* Network interfaces are now configured with the names *net0* and *net1* instead of *eth0* and *eth1*.
* **nftables** has replaced **iptables**. Use **systemctl restart nftables** instead of **service iptables restart**.
* **chrony** has replaced **ntpd**. Configuration files are located in /etc/chrony.cnf.
* **tmux** has replaced **screen**. Use **tmux attach** instead of **screen -r**.

# Uplogix Local Manager

## New Features and Improvements

### Improvement: Cisco ROMMON Recovery - Additional Devices Supported

ROMMON Recovery support has been added for:
* Catalyst 3650, 3850, 9300L switches
* Cisco 4300 routers
* ASR 1001-X router

> **For switches with dedicated management ports:** It is important to note which port the switch will source file transfers from and configure the Local Manager accordingly.

### Improvement: OS Management of IOS-XE switch stack in Install mode

When running IOS-XE version 16.x, upgrading an entire switch stack is now supported (Models 3850 and 93XX). â€œpackages.confâ€ is not pulled for storage on the Local Manager since it cannot be directly booted from. Candidate or standard OS .BIN file is promoted to Current upon successful push completion. IOS-XE release 16.X is officially supported.

**Note:** initiate **push OS** command from the Local Manager port connected to stack master/active switch.

**Note:** The booted file must be â€œpackages.confâ€ for this automated upgrade process to work correctly.

> **For switches with dedicated management ports:** It is important to note which port the switch will source file transfers from and configure the Local Manager accordingly. Use the IOS-XE command "ip (protocol) source-interface (interface)" to set the source interface on the switch.

### Improvement: OS Management of IOS-XE switch stack in Bundled mode

Uplogix also supports upgrading Catalyst 9300 and 3850 series switches and stacks when running in â€œbundledâ€ mode. During a **push OS** sequence, the candidate OS .BIN is propagated to all switch stack members and all member file systems are cleaned. IOS-XE release 16.X is officially supported.

**Note:** initiate **push OS** command from the Local Manager port connected to stack master/active switch.

> **For switches with dedicated management ports:** It is important to note which port the switch will source file transfers from and configure the Local Manager accordingly. Use the IOS-XE command "ip (protocol) source-interface (interface)" to set the source interface on the switch.

## Other Changes and Updates

* Support external USB Multi-tech CatM1 modem. It connects to the Local Managerâ€™s USB-A and C ports.
* Resolved an issue where an IKEv2 VPN would fail to establish a connection due to a â€œraceâ€ condition, under certain circumstances.
* Implemented additional logging when an LTE modem is reset.
* Uplogix devices now support RSA SHA2-256/512 SSH host keys.
* Improved POST parsing for Catalyst 3800 series IOS XE stacked switches.
* When a standard OS is defined but current OS is not defined for a managed device, OS recoveries for that device will utilize the standard OS file.
* PING command refactored to match standard syntax. Issue â€œPING ?â€ for command options.
* When running a PING device monitor against a Cisco IOS device, â€œvrf=\[vrfName\]â€ can be added after the IP address/hostname to specify which device VRF should be used during command execution.
* User information has been added to Local Manager generated SYSLOG messages.
* A Local Manager issued reboot command of a Cisco 800 series router identifies and accounts for an embedded AP when detected.
* The config init command, when run against the Local Managerâ€™s modem port, now supports selection of an external USB LTE modem.
* Support added for Multitech CatM1 LTE USB modem.
* Addressed the following Common Vulnerabilities and Exposures (CVEs):
	* CVE-2020-10769

# Uplogix Control Center
## New Features and Improvements

### Improvement: Security
* The operating system of the UCC has been upgraded from CentOS 6 to CentOS 8.
* Uplogix Terminal Application upgraded for SSH improvements.  All non-AES cipher options have been dropped.  Public key algorithms rsa-sha2-256 and rsa-sha2-512 have been added.
* Added support for Letâ€™s Encrypt certificates.  This improvement also applies to any certificate authority that uses the ACME certificate protocol.

### Improvement: Performance Enhancements
* The Dashboard and Inventory pages have been significantly improved when there are large amounts of data backing them.
* When upgrading a Local Manager either from the CLI or scheduled from the UCC, the file can transfer significantly faster (10x) than previously.  This improvement also applies to any operation using the â€œuccâ€ protocol to the UCC File Archive.
* Improved performance of data cleanup during UCC boot.

### Improvement: New Reports
* Modem detail information for the entire deployment. 
* The most recent GPS data associated with all managed devices across the entire deployment.
* Secondary Ethernet detailed configuration for the entire deployment.
* Dedicated Ethernet card installation information for the entire deployment.

## Other Changes and Updates
* Over 50 smaller bug fixes and updates to the Control Center and Uplogix Terminal Application
* Addressed the relevant following Common Vulnerabilities and Exposures (CVEs):
	* CVE-2017-2647, CVE-2017-12192, CVE-2019-17666, CVE-2020-0543, CVE-2020-8616, CVE-2020-8617, CVE-2020-8622, CVE-2020-10711, CVE-2020-14363, CVE-2020-15862

# Release Dates and Build Numbers
**Version 6.1**
* Release Date: January 15, 2021
* Build Number: 37253

