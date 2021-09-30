Uplogix, Inc. is pleased to announce the release of version 5.3.0 software for all models of the Uplogix Local Manager and for the Uplogix Control Center.

The following software features, improvements and fixes have been made in both the Local Manager and the Control Center software.

# Uplogix Local Manager Updates

## New Features and Improvements

**New Hardware:**  European/Australian LTE Internal Cellular Modem  

Uplogix now offers an internal LTE modem for the 500 and 5000 platforms that is certified for the European, Great Britain, Australia, and New Zealand markets.

**New Feature:** Support for MRV LX Series Switched Power Controllers

The Uplogix Local Manager now supports advanced management of MRV's LX series switched power controllers.

**Improvement:** More Efficient Configuration Backup For Cisco Devices

The advanced Cisco device driver now calculates the checksum of configuration files on Cisco devices during a configuration backup operations to determine if the device configuration is different than the current configuration stored on the Local Manager - time is not wasted backing up the configuration if it is the same.

## Issues Addressed in This Release

Addressed the relevant following Common Vulnerabilities and Exposures (CVEs) and security issues:

* CVE-2013-7424: The getaddrinfo function in glibc before 2.15 could allow DoS attack or arbitrary code execution.
* CVE-2015-5477: Address BIND9 TKEY assertion failure.
* CVE-2015-5364: The (1) udp_recvmsg and (2) udpv6_recvmsg functions in the Linux kernel before 4.0.6 do not properly consider yielding a processor, which allows remote attackers to cause a denial of service (system hang) via incorrect checksums within a UDP packet flood.
* CVE-2015-5366: The (1) udp_recvmsg and (2) udpv6_recvmsg functions in the Linux kernel before 4.0.6 provide inappropriate -EAGAIN return values, which allows remote attackers to cause a denial of service (EPOLLET epoll application read outage) via an incorrect checksum in a UDP packet.
* CVE-2015-7182: NSS ASN.1 decoder heap overflow when decoding constructed OCTET STRING.

Advanced Cisco IOS/IOS-XE Driver Fixes and Improvements

* Configuring a Local Manager port to manage a Cisco IOS/IOS-XE device, where the pull and push configuration methods uses a file transfer method rather than the console/CLI interface, no longer takes a really long time to failover to using the console if there is no network connectivity between the Local Manager and the managed device.
* Lengthened an OS update timeout value to avoid aborting an OS update due to longer than usual upgrade times such as microcode updates to Cisco 3750X or 3850 switches.
* Fixed an issue that might cause an OS update via TFTP to a 3750 stack of switches to fail to initiate. 
* Fixed an issue that could randomly cause the Cisco IOS driver to report that an OS update failed when it actually succeeded.
* Fixed an issue that can cause a config update to fail on Cisco IOS-XE devices when the configuration snippet being pushed deletes a locally defined username from the configuration.
* Fixed an issue that can cause our Cisco IOS driver to fail to backup an IOS-XE OS file from a device for the case of a longer OS filename. 

Advanced Cisco NX-OS Driver Fixes and Improvements

* Fixed an issue that caused a longer Nexus 7K Dual Supervisor OS upgrade operation to timeout before it was complete.
* Fixed an issue that can cause the state of the Uplogix port connected to the console port of the new active/old standby Nexus 7K supervisor to be listed as "unknown" after an NX-OS upgrade.
* Fixed an issue that caused pushing a startup-config to a Cisco Nexus switch via TFTP over a dedicated Ethernet connection to fail.
* Fixed an issue that can cause the Local Manager to report a failure while updating a Cisco Nexus switch running configuration when the configuration update was successful.
* Fixed an issue that could cause an OS policy alarm on a Cisco Nexus switch when the standard OS matches the current OS.
* Fixed Cisco IOS and NX-OS drivers so they can successfully upgrade a device that had no OS stored in flash because it previously loaded its OS via TFTP (i.e. boot TFTP).

A SSH pass through session to a managed device via the UCC CLI Applet (blue CLI button at port level) will not timeout if port forwarding is active.

Fixed an uncommon issue that can cause a Local Manager syncing its time with the UCC (rather than using NTP) to report that it's clock is out of sync with the UCC. 

Fixed an issue that prevented the configuration of multiple secure virtual ports to Avocent Universal Management Gateway devices.

## Known Issues in This Release

The **push startup-config** function is not currently supported for dual supervisor Nexus switches

# Uplogix Control Center (UCC) Updates

**New Feature:** Uplogix Deployment Overview

The Administration section of the UCC now provides a deployment overview page that lists all the Uplogix Local Managers with helpful information about these Local Managers such as status (such as alarming or out-of-band), serial number, model number, IP address, uptime, software version, last heartbeat timestamp, heartbeat state (not currently heartbeating, full heartbeat or minimal heartbeat), number of physical and virtual ports, SLV license information. This page also includes sorting and filtering capabilities.

<div class='ucc' />Administration > Deployment Overview</div>

**Improvement:**  Users Can Now Export User Session Logs, Device Configuration Files, Show Tech and POST Output 

User session logs are a complete log of everything a user does when logged into a Local Manager or passing through it to manage a connected device - this information is accessed in the â€˜Session Logs' section of the Local Manager summary page. In addition to being viewable for auditing purposes, session logs can now be exported as well.

Users can also now export a running configuration, a startup configuration, and the output of the â€˜show tech' command or the Power On Self Test (POST) log for the case where these artifacts are available on the Local Manager ports.

**Improvement:**  Port Forwarding Defaults Local Port Selection to Forwarded Port If Available 

User who use the CLI button to open an SSH session to a Local Manager and activate port forwarding will now find that the applet will set the local port on the users workstation to the same port as the forwarded port number when they activate port forwarding if that port is available on their workstation. For example, if a user forwards port 443 on a managed device to his workstation, the applet will use port 443 on the local workstation if it is available (i.e. https://127.0.0.1:443 on the local workstation).

## Issues Addressed in This Release

Addressed the relevant following Common Vulnerabilities and Exposures (CVEs) and security issues:

* CVE-2015-8000: A denial of service flaw was found in the way BIND processed certain records with malformed class attributes. 
* CVE-2015-5722: A denial of service flaw was found in the way BIND parsed certain malformed DNSSEC keys.
* CVE-2015-5477: Address BIND9 TKEY assertion failure.
* CVE-2015-1789: A specially crafted X.509 certificate or a Certificate Revocation List (CRL) could possibly cause a TLS/SSL server or client using OpenSSL
to crash.
* CVE-2015-1790: A specially crafted PKCS#7 input with missing EncryptedContent data could cause an application using OpenSSL to crash.
* CVE-2015-4000: A man-in-the-middle attacker could use this flaw to force the use of weak 512 bit export-grade keys during the key exchange, allowing them to decrypt all traffic.
* CVE-2015-5364: A remote attacker could potentially use a Linux kernel's networking implementation flaw to trigger an infinite loop in the kernel, resulting in a denial of service on the system. 
* CVE-2015-5366: A remote attacker could potentially use a Linux kernel's networking implementation flaw that triggers a denial of service in applications using the edge triggered epoll functionality.
* CVE-2015-6908: A flaw was found in the way the OpenLDAP server daemon (slapd) parsed certain Basic Encoding Rules (BER) data.
CVE-2015-3195: A memory leak vulnerability was found in the way OpenSSL parsed PKCS#7 and CMS data.
* RHSA-2015-1514: A flaw was found in the way BIND handled requests for TKEY DNS resource records.
RHBA-2015-1191: Previously, running the irqbalance daemon on Red Hat Enterprise Linux 5 in some cases unintentionally rewrote the interrupt request (IRQ) CPU mask and modified banned interrupt values.
* RHBA-2015-0949: Previously, when using NetApp filers as NFS servers, the rpc.statd daemon in some cases terminated unexpectedly.
* RHEA-2015-0958: The certificate store has been upgraded to include the changes contained in version 2.4 of the CA certificate list published by Mozilla.org as part of NSS 3.18.1. However, for compatibility reasons, several root CA certificates with an RSA key size of 1024 bits have been kept as trusted.
* RHBA-2015-1032: Previously, when a system with a large .rhosts file used the rsh shell to connect to a rlogind server, the authentication took very long to process or failed due to a timeout. This update adjusts the pam_rhosts_auth module so that it performs DNS lookups for host names only in .rhosts entries with matching users. As a result, rlogind authentication with large .rhosts files is in most cases significantly faster, and no longer times out.  


Fixed CLI Applet to show the green and red status colors for port forwarding when setting and applying the local port number.

Fixed the DNS settings page to allow domain name in the Domain Search field to begin with a number.

Fixed the Local Manager Properties page to ask if you want to save changes if you navigate away without saving changes.

## Known Issues in This Release

Resizing the CLI applet window (i.e. SSH session to a Local Manager using the CLI button) while it is streaming/writing output to the screen may cause the applet screen to go blank or stop responding.

