# Overview
This document provides an overview of the Uplogix LM80 and LM83X Local Managers.

Several key improvements have been made from the previous generation of hardware:

* 256GB NVMe solid state drive allows for storage of larger device operating systems in high density deployments
* OPAL-compliant, self-encrypting storage for maximum security
* Upgraded CPU and RAM
* SFP (fiber) port standard on both platforms (for bonded, in-band management only)
* Smaller form factor (LM80) supports 8x serial ports (+2 over previous Uplogix 500)
* Management USB port upgraded from USB-A to USB-C
* Larger form factor (LM83X) supports 3 expansion bays (+1 over previous Uplogix 5000)
* Maximum port density for LM83X is 56 (+18 over previous Uplogix 5000)
* LCD Keypad is now optional on LM83X (external, USB LCD Keypad also available)

<div class='warning' />WARNING: DO NOT Connect Power Over Ethernet (PoE) to any Local Manager serial port.
Doing so is likely to damage the port as well as the unit.</div>


# Uplogix LM80 Local Manager (Base Chassis)
The LM80 and LM83X share the same base chassis.

![Uplogix LM80 Diagram](https://uplogix.com/support/docs/img/6.0/uplogix-lm80-local-manager-diagram.png)

## Communication Option Slot
A modular communication option slot supports a number of secondary management network transports.

* Cellular Modems - multiple carrier options available
* V.92 Modem - for legacy POTS deployments
* SFP (fiber) Card (for bonded, in-band management only)
* RS-232 DB-9 Card - for Iridium satellite modems and other external modems

## Management Network Connectivity
The Local Manager's management network operates in bonded mode by default and supports the following interfaces:

* 2x 10/100/1000 BaseT Ethernet 
* 1x SFP (fiber)

## Management Console Connectivity

The Local Manager has a standard RJ-45 RS-232 console port operating at 9600, 8N1 for configuration. A USB-C port is provided for connection to a PC. See Connecting a Local Manager to a Windows PC.

## USB Port

A USB-A port allows for the attachment of peripherals such as a temperature/humidity sensor, LCD Keypad, or USB drive.

## Device Management Ports

The Local Manager has 8 built-in serial console ports for connecting to managed devices such as routers, switches, firewalls, etc. Device management ports operate in DCE mode.

Ports are organized into physical slots. On both the LM80 and LM83X, the 8 fixed ports on the base chassis comprise Slot 1.

# Uplogix LM83X Local Manager (Modular Chassis)
The Uplogix LM83X contains all of the hardware features available on the LM80 (see above). The wider chassis of the LM83X allows for higher density device management and enhanced configuration options.

![Uplogix LM83X Diagram](https://uplogix.com/support/docs/img/6.0/uplogix-lm83x-local-manager-diagram.png)

## Modular Design

A modular chassis allows for the installation of three additional [expansion cards](https://uplogix.com/docs/local-manager-user-guide/series-8/expansion-cards). 

The chassis is divided into slots numbered from left to right, with the built-in 8 serial ports occupying slot 1. Slots 2, 3, and 4 will map to cards inserted in the respective bays. Slot 5 is reserved for [Virtual Ports](https://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/using-virtual-ports).

## Device Management Ports

The LM83X has 8 built-in serial console ports for connecting to managed devices. With a fully populated chassis, the LM83X can manage up to 56 directly connected devices.

## LCD Display and Keypad

Unlike the previous high density Local Manager, the Uplogix 5000, the LM83X does not have a built-in LCD and Keypad. This functionality is now handled by an optional card. See [LCD Screen and Keypad Expansion Card](https://uplogix.com/docs/local-manager-user-guide/series-8/lcd-screen-and-keypad-expansion-card) for more information.