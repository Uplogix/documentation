# Overview

Uplogix, Inc. is pleased to announce the release of version 6.2 software for the Uplogix Local Manager and for the Uplogix Control Center.

The following software features, improvements and fixes have been made in both the Local Manager and the Control Center software.

This document covers LMS version 6.2 and all subsequent patch sub-releases. Changes made in patch releases are marked with the version number.

# Requirements

* LMS 6.2 is supported on Uplogix 500, 5000, LM80, LM83X, and Virtual Local Managers. Previous hardware platforms are not supported.
* LMS 6.2 supports upgrades from version 6.1.x only.
* LMS 6.2 is not supported on Control Centers running on Dell 2850, 2950, or R710 servers.

# Uplogix Local Manager
## New Features and Improvements

### Improvement: OS Management of IOS-XE switch stack

The Local Manager has improved awareness and understanding regarding Cisco switch stacks. When a device port is initialized, the Local Manager will determine if the port is connected to the console of a stack “Active” or “Non-Active” switch and respond accordingly:

* Active switch device ports will initialize in typical fashion for a Cisco IOS -XE switch and execute the resulting monitors. 
* Non-Active device ports will initialize with default monitors, per usual, but those monitors will not automatically execute against the stack member. 

The Local Manager will periodically determine the role of the switch it is locally polling. If any member switch becomes “Active,” the dormant monitors will activate and execute against the switch.

If manual commands, such as **terminal**, **pull configuration**, etc., are executed against a non-active switch, the user will be notified that the directly connected switch is not active, and that the command was not executed.

### Improvement: Support of Cisco ASA in explicit FIPS mode

The Local Manager now fully negotiates FIPS-compliant ciphers, hashes, etc. with Cisco ASAs placed into their “FIPS mode” via the ASA’s “fips enable” command. This permits Local Managers to establish IKEv2/IPsec certificate-based VPNs with ASAs running in this mode.

## Other Changes and Updates

* Users can now run the *pull tech* command against an LTE modem that provides at least two USB channels while the modem is outband with an active PPP session. The results can be viewed, with timestamp, in the modem context, via the **show directory -v** command.
* Upon startup of a Local Manager with an LTE modem installed, several default monitors will be applied and enabled against that modem. This improves the effectiveness of other interactions between the Local Manager and modem.
* Local Manager automated device interactions now correctly identify if a switch named “switch” is part of a stack.
* CVE-2020-25681 through CVE-2020-25687 (dnsmask)k)

# Uplogix Control Center
## New Features and Improvements
### Feature: Virtual UCC Supported in Microsoft Azure

The virtual Control Center is now operationally supported within the Microsoft Azure cloud environment. A guide is available to assist with your deployment needs. Please contact Uplogix Support when you are ready to deploy.

## Changes and Updates
* UCC operating system migrated to Alma Linux 8 in response to an unexpected December 2021 End-Of-Support announcement. Uplogix moved to Alma because of its strong community support, functional equivalence to Redhat releases, and announced development support until at least 2029.
* Minor UI usability improvements.
* Over 50 smaller bug fixes and updates to the Control Center and Uplogix Terminal Application
* Addressed more than 80 kernel-based Common Vulnerabilities and Exposures since release 6.1.0 to strengthen OS security.
* Addressed more than 125 non-kernel Common Vulnerabilities and Exposures since release 6.1.0 to strengthen OS security.

# Release Dates and Build Numbers

## Version 6.2
* Release Date: September 10, 2021
* Build Number: 
