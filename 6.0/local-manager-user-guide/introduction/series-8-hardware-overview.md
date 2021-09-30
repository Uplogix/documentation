# Platform Overview
This document provides an overview of the Uplogix LM80 and LM83X Local Managers released in 2020.

Several key improvements have been made from the previous generation of hardware:

* 120GB NVMe solid state drive allows for storage of larger device operating systems in high density deployments
* OPAL-compliant, self-encrypting storage for maximum security
* Upgraded CPU and RAM
* SFP (fiber) port standard on both platforms
* Smaller form factor (LM80) supports 8x serial ports (+2 over previous Uplogix 500)
* Management USB port upgraded from USB-A to USB-C
* Larger form factor (LM83X) supports 3 expansion bays (+1 over previous Uplogix 5000)
* Maximum port density for LM83X is 56 (+18 over previous Uplogix 5000)
* LCD Keypad is now optional on LM83X (external, USB LCD Keypad also available)

## Uplogix LM80 Local Manager (Base Chassis)

The LM80 and LM83X share the same base chassis.

![Uplogix LM80 Diagram](https://uplogix.com/support/docs/img/6.0/uplogix-lm80-local-manager-diagram.png)

### Communication Option Slot
A modular communication option slot supports a number of secondary management network transports.

* Cellular Modems - multiple carrier options available
* V.92 Modem - for legacy POTS deployments
* SFP (fiber) Card
* RS-232 DB-9 Card - for Iridium satellite modems and other external modems

### Management Network Connectivity
The Local Manager's management network operates in bonded mode by default and supports the following interfaces:

* 2x 10/100/1000 BaseT Ethernet 
* 1x SFP (fiber)

### Management Console Connectivity

The Local Manager has a standard RJ-45 RS-232 console port operating at 9600, 8N1 for configuration. A USB-C port is provided for connection to a PC. See Connecting a Local Manager to a Windows PC.

### USB Port

A USB-A port allows for the attachment of peripherals such as a temperature/humidity sensor, LCD Keypad, or USB drive.

### Device Management Ports

The Local Manager has 8 built-in serial console ports for connecting to managed devices such as routers, switches, firewalls, etc. Device management ports operate in DCE mode.

Ports are organized into physical slots. On both the LM80 and LM83X, the 8 fixed ports on the base chassis comprise Slot 1.

## Uplogix LM83X Local Manager (Modular Chassis)

![Uplogix LM83X Diagram](https://uplogix.com/support/docs/img/6.0/uplogix-lm83x-local-manager-diagram.png)

* Modular design
* Slot Numbering

The Uplogix Local Manager provides buttons and indicator lights for in-person configuration and troubleshooting. LEDs are multi-color and can flash at various speeds or remain solid. The LM80 and LM83X have identical functionality. 

## System Buttons

### Power Button
Press to power on the Local Manager. Hold to restart the Local Manager.

### Reset Button
The reset button can be used to factory reset the Local Manager. Hold before applying power to begin the factory reset.

## Indicator Lights
### Power LED
This LED will light a solid green when the system is powered on.

### Status LED
During normal operation, the status LED presents the following colors:
* White (solid): BIOS loading
* Yellow (flashing): operating system loading
* Green (flashing): application loaded and running

### Warning LED

The warning LED works in conjunction with the status LED to indicate events outside of normal operation.

| Â  | Warning LED | Status LED |
| --- | ----------- |----------- |
| Software Installing	| BLUE (flashing)	| BLUE (solid) |
| Factory Reset | Beginning	BLUE (flashing)	| YELLOW (solid) |
| Factory Reset | Running	GREEN (rapid flashing)	| BLUE (solid) |
|FIPS | Warning	RED (flashing) | RED (flashing) |

# LCD Screen and Keypad Expansion Card
The Uplogix LM83X Local Manager supports an LCD screen and keypad through an optional expansion card. The keypad can be used to configure the Local Manager without the need for a workstation. After configuration, the LCD screen displays system messages during boot and status information during normal operation.

## Using the keypad

The keypad consists of four arrow buttons, an Enter button (located in the center), and a Back button. The left and right arrow keys move the cursor left and right, respectively. The up and down arrow keys change numerical values.

![Uplogix LM83X LCD](https://uplogix.com/support/docs/img/6.0/lm83x-lcd.png)

When the Local Manager is powered on, press the Enter key in the center of the keypad to display the menu. Press the Back key below the left arrow key to exit the menu and resume scrolling status information.

The menu functions include:

### Configure

The Configure menu allows configuration of basic network and system settings. These settings include:

* IP Addressing - set the IP address, subnet mask, and default gateway 
* Control Center - set the IP address of your Uplogix Control Center
* Pulse IP - set the IP address of your Pulse server

### Restart

Restarts the Local Manager. Equivalent to the **restart** command
 
### Shutdown

Powers off the Local Manager. Equivalent to the **shutdown** command

### Update

Initiates a system upgrade from a USB flash drive. This option is available only if a USB flash drive is connected to the Local Manager. Equivalent to the **config update usb** command.

### Factory reset (hidden below two blank lines)

Restores the Local Manager to its initial state. Equivalent to the **config reinstall** command.

## Viewing Status Information

During normal operation, the LCD screen will cycle through various messages, including:

* Software Version
* Uplogix Status (Good, Out-of-Band, Upgrading, Alarms Exist, etc.)
* IP Address
* Control Center IP Address
* Pulse Server IP Address
* Port Information (hostname or description)

During the boot process, the LCD screen will display system messages.

In the event of a software or hardware error, the LCD screen may display the Uplogix logo or the Local Manager's serial number.

# Expansion Cards
Expansion cards (also known as *option cards*) add serial and Ethernet ports to the Local Manager. The Uplogix LM83X supports three expansion cards for a maximum serial port density of 56. 

## LCD Card

![](https://uplogix.com/support/docs/img/6.0/lm83x-lcd.png)

The LCD screen and menu buttons have been moved to a modular card that can be installed in any expansion slot. 

## 8 Port Serial Card

![LM83X 8 Port Serial Card](https://uplogix.com/support/docs/img/6.0/lm83x-8-port-serial.png)

The 8 Port Serial Card adds 8 serial ports to the LM83X.

## 16 Port Serial Card

![](https://uplogix.com/support/docs/img/6.0/lm83x-16-port-serial.png)

The 16 Port Serial Card is used with 8 Port fan-out cables that have a v.68M connector for attaching to the card and 8 RJ-45 connectors pinned as DCE. Two of these cables can be used to connect the card to up to 16 devices. 

### 8 Port Fan-out Cable

![](http://uplogix.com/support/docs/img/installing-a-local-manager/fan-out-cable_with-stickers.png)

The fan-out cables come with a set of stickers for labeling. Wrap the stickers on the ferrite bead near the RJ45 connectors as shown above. The stickers allow you to label the cables with both slot and port numbers for easier identification. 

**IMPORTANT:** The numbering of the fan-out cables may not be in order from left to right. **ONLY** rely on the numbers on the labels at the end of the cables.  

## 8 Port Dedicated Ethernet Card

![](https://uplogix.com/support/docs/img/6.0/lm83x-8-port-ethernet.png)
# Physical Installation
**Please read the [Uplogix Safety Summary](http://uplogix.com/docs/local-manager-user-guide/reference/safety-summary) before proceeding with installation.**

## Site Requirements

Ensure that the power source meets the following requirements:

* Provides appropriate power (AC or DC) as required by the Local Manager
* Provides overload protection
* Is connected to earth ground

<div class='danger'>The power source must meet all requirements to ensure safe and reliable operation.</div>

Ensure the installation site ambient temperature does not exceed 113F (45C) or fall below 32F (0C).

<div class='warning'>The unit will overheat if the sites does not meet these requirements.</div>

## Optional equipment

The following optional equipment is available for Uplogix Local Managers.

* v.92 modem
* DB-9 (RS-232) serial module
* Cellular modem
* SFP (fiber) module

<div class='info'>Most optional equipment is factory installed and is ready to use when the Local Manager is unboxed.</div>

### Install a v.92 modem

Follow these steps if a v.92 modem is not already installed in the option slot.

1.	Power off the Local Manager.
2.	Remove the option slot cover, align the modem carrier card with the internal rails, and slide the modem into place.
3.	Replace the screws.
4.	Connect a POTS telephone line to the RJ-11 jack on the modem
5.	Power on the Local Manager.

![v92 modem diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image007.png)

### Install a DB-9 serial module

The DB-9 serial module is used in the following scenarios:

* External v.92 modem
* External standalone Iridium (9522B)
* Uplogix LEO-I Kit
* External cellular modems

Follow these steps if a DB-9 serial module is not already installed in the option slot.

1.	Power off the Local Manager.
2.	Remove the option slot cover, align the DB-9 card with the internal rails, and slide the card into place.
3.	Replace the screws.
4.	Power on the Local Manager.

![DB-9 serial module diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image009.png)

### Install a GPRS cellular modem

Follow these steps to install the GPRS cellular modem:

1.	Power off the Local Manager.
2.	Install an activated SIM card on the modem.
3.	Remove the option slot cover, align the modem carrier card with the internal rails, and slide the modem into place.
4.	Feed wire into the option slot compartment, align modem cover plate with the option slot screw holes, and replace the screws.
5.	Install antenna.
6.	Power on the Local Manager.

![GPRS cellular modem diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image008.png)

### Install a CDMA cellular modem

Follow these steps to install the CDMA cellular modem:

1.	Power off the Local Manager.
2.	Note the Electronic Serial Number (ESN) on the modem, as this will be needed in order to activate the modem on your carrier's network.
3.	Remove the option slot cover, align the modem carrier card with the internal rails, and slide the modem into place.
4.	Feed wire into the option slot compartment, align modem cover plate with the option slot screw holes, and replace the screws.
5.	Install antenna.
6.	Power on the Local Manager.

![CDMA cellular modem diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image008.png)

### Install an SFP module

Follow these steps to install the SFP module:

1.	Power off the Local Manager
2.	Remove the option slot cover, align the carrier card with the internal rails, and slide the module into place.
3.	Replace the screws.
4.	Install either a 1000Base SX (GLC-SX-MM) SFP or the 1000Base LX/LH (GLC-LH-SM) SFP for fiber connectivity. Both the 1000Base SX (GLC-SX-MM) SFP and the 1000Base LX/LH (GLC-LH-SM) SFP are customer-provided equipment. 

<div class='info'>SFP modules are hot swappable, but the SFP carrier option card is not hot swappable.</div>

![SFP module diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image010.png)

### Install a temperature and humidity sensor

Environmental monitoring is available via a USB-connected temperature and humidity sensor.

Follow these steps to connect the sensor. Note the Local Manager does not need to be powered down for installation of this sensor.

1.	Plug the sensor into one of the two USB connections on the Local Manager.
2.	Place sensor collection end in the area you wish to collect environmental information, ideally not near a fan or on hot equipment.

It may take up to 10 minutes for the sensor to normalize to the environmental temperature and begin reporting consistent data. 

## Install expansion cards
Use the following procedure to install or replace an expansion card.

<div class='warning'>Always power off the Local Manager before installing or removing expansion cards.</div>

1.	Power off the Local Manager.
2.	Using a #2 Philips screwdriver, loosen the module screws securing the blank faceplate or the option card to be replaced and remove it.
3.	Slide the new or replacement option card into place. Ensure the two module retention screws are threaded into the faceplate of the card. The screws will align to holes in the chassis if the screws are slightly backed out of the front panel. 
<div class='info'>Installing the option card with the screws fully engaged makes it difficult to install the card properly.</div> 

4.	Look inside the chassis and find two tabs close to the front of the option slot and two located further back. Place the rear edge of the card on the two front tabs, tilt the card up and slide it back so the card edges slide below the two rear tabs. Gently push the card back until the card seats in the connector on the backplane.
<div class='warning'>If it is difficult to slide the card or if the card resists being properly seated, the card is probably not installed correctly. Remove the card and start over. Very little force is required to install the cards.</div>

5.	Tighten the module retention screws to ensure that the internal connector seats properly. 
<div class='warning'>Over tightening the screws may strip the threads and is not required; finger tight is sufficient. As you install the retention screws, you may encounter some resistance. If needed, use a #2 Philips screwdriver to overcome this resistance but use care not to cross thread or strip the screw.</div>
6.	If you are installing a 16 port serial card, attach the supplied octopus cable to the connector on the front of the card.

## Install chassis in rack

Uplogix Local Managers are designed for standard 19-inch telco racks.

The Uplogix 500 ships with rubber standoffs for desktop use.

### Uplogix LM83X

To mount the Local Manager in a rack:

1. Use the included screws to attach the mounting brackets.
![Uplogix 5000 Rack Brackets](http://uplogix.com/support/docs/img/installing-a-local-manager/image025.png)
2. Mount the Local Manager in the rack

### Uplogix LM80

To mount the Local Manager with the optional center-mount kit:

1.	Attach the mounting brackets.
2.	Mount the Local Manager in the rack.
![Uplogix 500 Center Mount](http://uplogix.com/support/docs/img/installing-a-local-manager/image012.png)

## Connect to power

Before connecting the Local Manager to power, ensure all [site requirements](#site-requirements) are met.

Connect the power cord to the Local Manager. Use either the provided power cord or one that is suitable for your location. The Uplogix Local Manager uses a power cord with a standard IEC-320-C13 female cord end.

![A Power Cord](http://uplogix.com/support/docs/img/lm-user-guide/plug.png)
 
Connect the power cord to a power outlet. A dimly lit keypad and dark display (if installed) indicates that the unit has power applied. Power the unit on by pressing the middle keypad button. The display on the front panel will illuminate and display progress messages as the device boots. At the end of the boot sequence, it displays the message **Uplogix status good**.

## Installation complete

You are now ready to complete the initial setup of the Uplogix Local Manager.
