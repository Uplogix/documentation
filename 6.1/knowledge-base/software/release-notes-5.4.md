<!-- 5.4 -->

Uplogix, Inc. is pleased to announce the release of version 5.4 software for all models of the Uplogix Local Manager and for the Uplogix Control Center.

The following software features, improvements and fixes have been made in both the Local Manager and the Control Center software.

This document covers LMS version 5.4 and all subsequent patch releases. Changes made in patch releases are marked with the version number.

<div class='danger' />This software will not run on newer Local Managers, including the Uplogix LM80 and LM83X.</div>

# Uplogix Local Manager Updates

## New Features and Improvements

### New Feature: Local Manager Secure Tunneling to UCC

A Local Manager can now be configured to establish a reverse SSH tunnel back to the UCC over in-band and out-of-band connections that will carry SSH terminal connections to it (with UCC acting as a proxy) in order to overcome network address translation (NAT) and other issues that can make it unreachable when initiating a SSH session to it. When in place, the Local Manager can optionally be configured to no longer listen to port 22 for SSH connections as an additional security measure.

For more information, see [Reverse SSH Tunnels](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/reverse-ssh-tunnels)

### New Feature: SSH-VTY Virtual Ports

SSH-VTY virtual ports establish secure connections to managed devices such that Uplogix monitoring and automation will use the port configured credentials to access the managed device, whereas anyone else (without the permission "use system auth") must use their own credentials when accessing these managed devices.

### New Feature: Connectionless Virtual Ports

Connectionless virtual ports were added to simplify management for devices like service processors where users simply desire to use the SSH TCP port-forwarding feature to forward the GUI and other application ports without making an actual SSH or telnet virtual connection to the device.

### New Feature: Manage Multiple Switched Power Controllers

Pre version 5.4 software releases only support advanced power controller management on one serial port (port 1/6). Any port, including virtual ports, can now be configured to manage switched power controllers on the 500/5000 platforms.
 
### Improvement: Port 1/6 is No Longer Dedicated to Power Control

Serial port 1/6 on the 500/5000 platforms is now a generic device management port like the rest of the serial ports on these platforms â€“ i.e. it can be configured to manage any supported device make and OS, including switched power controllers.

### Improvement: Added Local Manager IP Address Variable for Generic Pull TFTP Function
 
The pullTFTP function allows users to define and schedule jobs to backup OS and configuration files from devices to the Local Manager using the TFTP protocol (for the case where there is no existing driver that already does this). A new variable has been added that can be used in the TFTP copy command to be run on the managed device, where the driver will automatically substitute the current Local Manager IP address into command to copy the file off the managed device to the Local Manager.

### Other Changes and Issues Addressed in This Release

* Advanced Cisco IOS/IOS-XE Driver Fixes and Improvements:
	* Local Manager port settings now include the SFTP protocol among the file transfer protocols that can be specified for this driver to use when backing up and restoring configuration and OS images between the Local Manager and the managed device.
	* New functionality was added to validate the current OS referenced by the boot variable on the managed device â€“ an alarm is generated if the driver finds the referenced OS image missing from the device.
	* Improved the driver to validate and free up space if possible on stacked switches during an OS upgrade.
	* Fixed an issue that could falsely report an OS upgrade failure on stacked switches in situations where the network does not converge quickly after reloading the stack.
	* Fixed a race condition issue that could have resulted in the driverâ€™s failure to pull the managed device running-config file after a terminal session.
	* Fixed an issue that could cause the driver to fail to back up the OS during a **config init** operation when using FTP to transfer the OS from a 3850 switch.
	* Fixed an issue where the driver falsely reports that it failed to push a running-config to a 3850 with no configuration.
	* Fixed a sporadic issue that could cause a failure during ROMMON recovery on an ISR platform.
* Advanced Cisco NX-OS Driver Fixes and Improvements:
	* Improved our Cisco NX-OS driver to better manage Nexus 9000 platforms:
		* Updated push OS functionality to make OS upgrades work.
		* Fixed parsing version information.
	* New functionality was added to validate the current OS referenced by the boot variable on the managed device â€“ an alarm will be generated if the driver finds the referenced OS image missing from the device.
	* Fixed an issue that left staged rollback configuration snippets in flash on the Nexus switch
* The Uplogix 5000 display behavior changes with this software release.  It will be brightly lit during use and will then dim to 10% of its brightness after being idle for 15 minutes.  Pressing any key on the keypad will wake the display up to full brightness.
* Addressed the relevant following Common Vulnerabilities and Exposures (CVEs):
	* CVE-2016-1950: NSS heap-based buffer overflow flaw in ASN.1 parsing of certificates.
	* CVE-2015-8000: A denial of service flaw was found in the way BIND processed certain records with malformed class attributes.
	* CVE-2015-8704: A denial of service flaw was found in the way BIND processed certain malformed Address Prefix List (APL) records.
	* CVE-2016-1285: A denial of service flaw was found in the way BIND processed certain control channel input.
	* CVE-2016-1286: A denial of service flaw was found in the way BIND parsed signature records for DNAME records.
	* CVE-2016-2848: A denial of service flaw was found in the way BIND handled packets with malformed options.
	* CVE-2016-8864: A denial of service flaw was found in the way BIND handled responses containing a DNAME answer.
* (**5.4.1**) Advanced Cisco IOS/IOS-XE Driver Fixes and Improvements:
	* Fixed an issue that falsely reports a missing managed device OS for the case where the Cisco IOS-XE device is running in installed mode (i.e. it uses the packages.conf file instead of a â€œ.binâ€ OS file)
	* Fixed a detect device state issue with this driver that could interrupt the boot process after a system restart, causing this driver to then initiate an unnecessary recovery process. 
* (**5.4.1**) Addressed the relevant following Common Vulnerabilities and Exposures (CVEs):
	* CVE-2016-9147: A denial of service flaw was found in the way BIND handled a query response containing inconsistent DNSSEC information. A remote hacker could use this flaw to make the named process exit unexpectedly with an assertion failure via a specially crafted DNS response.
	* CVE-2016-7429: A flaw was found in the way ntpd running on a host with multiple network interfaces handled certain server responses. A remote attacker could use this flaw that would cause ntpd to not synchronize with the source.
	* CVE-2016-7433: A flaw was found in the way ntpd calculated the root delay. A remote attacker could send a specially-crafted spoofed packet to cause denial of service or in some special cases even crash.
* (**5.4.2**) Push OS improvements with Cisco IE and un-stacked 3750s.
* (**5.4.3**) No changes were made to the Local Manager in this patch, but it is recommended to upgrade for consistency and ease of deployment management.


## Known Issues in This Release

* The Local Manager dashboard will show an SSH-VTY virtual port as unavailable after a â€˜Replaceâ€™ operation from the UCC until a job runs on that port, a user interacts with the port or until a Local Manager restart happens.

# Uplogix Control Center (UCC) Updates

## Improvement: SSH for Dial Applet 

Added an SSH choice for call setup to the modem server to encrypt applet to modem server communication when dialing into a Local Manager modem.

## Improvement:  Power Controller Visibility and Outlet Mapping  

Now it is easy to see what device ports are connected to power controllers and what ports are mapped to power controller outlets for power control from the Local Manager device summary page. The port/device cards in the â€˜Devicesâ€™ section on the Local Manager summary page include a lightning bolt icon in the upper right corner if the device is a managed power controller and a universal power button icon is present if the managed device is mapped to one or more managed power controller outlets.

Additionally, all power outlet to device port mappings for a given power controller are now shown at the top of the power controller port summary page in the â€˜Outletsâ€™ section. If a device is mapped to a power controller outlet, the device summary page will indicate the power controller port on the Local Manager that is providing power control for it.


## Improvement:  Track and Display Standby UCC Synchronization State 

The â€˜Install Informationâ€™ section of the UCC Administration -> Server Settings page has been updated to track and display the status of the standby UCC, allowing users to see if UCC high availability is configured, and if so, whether or not the standby UCC is in sync with the active UCC.

## Improvement: The Uplogix Virtual Control Center Software Now Includes VM Tools 

Uplogix is bundling VM tools with the virtual UCC (vUCC) software from this release forward in order to improve VM performance and manageability. The software upgrade process will uninstall any version of VM tools it finds and replace it with the version of VM tools bundled in the Control Center software.

## Improvement:  OS Policies For IOS Devices Can Be Defined at the Supervisor Level  

Previous releases only identified down to the chassis model number for managed devices, thus limiting users to having one OS policy for a given chassis model, where it is possible for some device models to have different supervisor engines that run different code versions. The Local Manager now recognizes and includes Cisco supervisor engine information in the device type when applicable, allowing users to define a policy based on the supervisor engine in a given platform.

## Other Changes and Issues Addressed in This Release

* The user interface was cleaned up to remove redundant CLI button functionality for the Local Manager and the managed devices/ports.
* The â€˜CLIâ€™ buttons were renamed to â€˜SSHâ€™ or â€˜Terminalâ€™ based on their use.
* The â€˜use system authâ€™ permission has been removed from the admin role that ships with the Uplogix Control Center (UCC).  When upgrading from a previous release, a new role named â€˜use_system_authâ€™ will be added and new privileges created that use this role everywhere there is a privilege that references the â€˜adminâ€™ role. This is done to guarantee systems upgrading from earlier releases behave the same.   The â€˜use system authâ€™ permission causes the system to use the credentials configured on the Local Manager port to log into a managed device when a terminal session is initiated by a user rather than making the user enter his/her own user credentials to access the managed device in the terminal session.
* Fixed a display issue in the UCC that could sporadically indicate that a Local Manager was not consistently communicating with the UCC (i.e. the Local Manager icon could flap between green and gray) for the case where the Local Manager heartbeat interval was increased to 120 seconds or greater (from the default of 30 seconds).
* Updated the terminal app certificate to overcome problems caused by more strict security requirements in newer versions of Java that could prevent the SSH and Dial applets from working or require users to change their Java security settings.
* Fixed an uncommon issue that can cause the SSH applet window to freeze up or go blank when a user resizes the window at just the right time as data is being output to the window from the Local Manager.
* Fixed the SSH and Dial applets to properly interpret the AltGr key on AZERTY keyboards that is required to produce the @ sign.
* Fixed an issue that might result in defining ports on an Uplogix 5000 that exist only on a 3200 when performing a replace operation where an Uplogix 3200 is replaced with an Uplogix 5000.
* Fixed an issue where uploading a newer version of a file to the UCC File Archive with the same name and category does not result in the new version of the file being used for scheduled jobs.
* Addressed the relevant following Common Vulnerabilities and Exposures (CVEs):
	* CVE-2014-1491: It was found that NSS accepted weak Diffie-Hellman Key exchange (DHKE) parameters.
	* CVE-2016-3081: Apache Struts 2.x before 2.3.20.2, 2.3.24.x before 2.3.24.2, and 2.3.28.x before 2.3.28.1, when Dynamic Method Invocation is enabled, allow remote attackers to execute arbitrary code via method: prefix, related to chained expressions.
* Addressed several issues by upgrading Tomcat from 6.0.44 to 7.0.73.
* (**5.4.1**) Addressed the relevant following Common Vulnerabilities and Exposures (CVEs):
	* CVE-2016-9147:  A denial of service flaw was found in the way BIND handled a query response containing inconsistent DNSSEC information. A remote attacker could use this flaw to make named exit unexpectedly with an assertion failure via a specially crafted DNS response.
	* CVE-2016-8864:  A denial of service flaw was found in the way BIND handled responses containing a DNAME answer. A remote attacker could use this flaw to make named exit unexpectedly with an assertion failure via a specially crafted DNS response.
	* CVE-2016-2848:  A denial of service flaw was found in the way BIND handled packets with malformed options. A remote attacker could use this flaw to make named exit unexpectedly with an assertion failure via a specially crafted DNS packet.
	* CVE-2016-2776:  A denial of service flaw was found in the way BIND constructed a response to a query that met certain criteria. A remote attacker could use this flaw to make named exit unexpectedly with an assertion failure via a specially crafted DNS request packet.
	* CVE-2016-0718:  An out-of-bounds read flaw was found in the way Expat processed certain input. A remote attacker could send specially crafted XML that, when parsed by an application using the Expat library, would cause that application to crash or, possibly, execute arbitrary code with the permission of the user running the application.
	* CVE-2016-8635:  It was found that Diffie Hellman Client key exchange handling in NSS was vulnerable to small subgroup confinement attack. An attacker could use this flaw to recover private keys by confining the client DH key to small subgroup of the desired group.
	* CVE-2016-7545:  It was found that the sandbox tool provided in policycoreutils was vulnerable to a TIOCSTI ioctl attack. A specially crafted program executed via the sandbox command could use this flaw to execute arbitrary commands in the context of the parent shell, escaping the sandbox.
	* CVE-2016-7032:  It was discovered that the sudo noexec restriction could have been bypassed if application run via sudo executed system() or popen() C library functions with a user supplied argument. A local user permitted to run such application via sudo with noexec restriction could use this flaw to execute arbitrary commands with elevated privileges.
	* CVE-2016-7076:  It was discovered that the sudo noexec restriction could have been bypassed if application run via sudo executed wordexp() C library function with a user supplied argument. A local user permitted to run such application via sudo with noexec restriction could possibly use this flaw to execute arbitrary commands with elevated privileges.
	* CVE-2016-1248:  A vulnerability was found in vim in how certain modeline options were treated. An attacker could craft a file that, when opened in vim with modelines enabled, could execute arbitrary commands with privileges of the user running vim.
	* CVE-2016-7426:  It was found that when ntp is configured with rate limiting for all associations the limits are also applied to responses received from its configured sources. A remote attacker who knows the sources can cause a denial of service by preventing ntpd from accepting valid responses from its sources.
	* CVE-2016-7429:  A flaw was found in the way ntpd running on a host with multiple network interfaces handled certain server responses. A remote attacker could use this flaw that would cause ntpd to not synchronize with the source.
	* CVE-2016-7433:  A flaw was found in the way ntpd calculated the root delay. A remote attacker could send a specially-crafted spoofed packet to cause denial of service or in some special cases even crash.
	* CVE-2016-9310:  A flaw was found in the control mode functionality of ntpd. A remote attacker could send a crafted control mode packet, which could lead to information disclosure or result in DDoS amplification attacks.
	* CVE-2016-9311 A flaw was found in the way ntpd implemented the trap service. A remote attacker could send a specially crafted packet to cause a null pointer dereference that will crash ntpd, resulting in a denial of service.
* (**5.4.1**) Upgraded Tomcat from 7.0.73 to 7.0.75.
* (**5.4.2**) Patched critical Struts vulnerability "Strutshock" (CVE-2017-5638).
* (**5.4.2**) Improved Dial-in when using SOCKS.
* (**5.4.3**) Fixed SSH, Terminal, and Dial-in applications to work with JRE 1.8 update 141+.
	* While JRE versions 1.8 update 51 through 1.8 update 131 work with most versions of the Control Center (including 5.4.0, 5.4.1, 5.4.2, and 5.4.3), it is recommended to upgrade your client JRE to the latest version.  With version 141 and after (ex. 151, 161, 171), patch version 5.4.3 is required.  If needed, JRE 1.7 update 80 can be made to work with some configuration.  For more information, please contact Uplogix Support.  JRE 1.7 update 40 is no longer supported.
	
# Release Dates and Build Numbers

### Version 5.4.0
* Release Date: 12/19/2016
* Build Number: 30647

### Version 5.4.1
* Release Date: 2/17/2017
* Build Number: 30876

### Version 5.4.2
* Release Date: 6/14/2017
* Build Number: 31553

### Version 5.4.3
* Release Date: 7/26/2017
* Build Number: 31895

