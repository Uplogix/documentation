# Overview

This guide describes the procedures for installing the Uplogix LEO-I remote satellite modem and GPS kit. This information is applicable for both revisions of the Above Deck Unit PCB.

# Verify LEO-I Kit Revision

This document is written for the 2019 revision of the LEO-I Kit. To verify your version, look for **UP620063 REV** in the upper left corner of the PCB inside the ADU. The copyright date should be **2019**.

# Diagrams and Photos

## Above Deck Unit (ADU)

![Above Deck Unit](https://uplogix.com/support/docs/img/6.1/leo/antenna-assembly-2.jpg)

## Below Deck Unit (BDU)

![Below Deck Unit](https://uplogix.com/support/docs/img/6.1/leo/bdu.jpg)

# Required Equipment

## SIM Card

A valid and active SIM card is required for access to the Iridium satellite network. Contact your Service Provider if you do not have a SIM card.

## Uplogix Local Manager

Uplogix 500/5000 models have modem option slots on the front of the chassis and must have an RS-232 module installed 

![Uplogix 500/5000 Option Slot Diagram](https://uplogix.com/support/docs/img/6.1/lm5k-option-slot-diagram.png)

Uplogix LM80/LM83X models have modem option slots on the front of the chassis and must have an RS232 module installed.

![Uplogix LM80/LM83X Option Slot Diagram](https://uplogix.com/support/docs/img/6.1/lm8k-option-slot-diagram.jpg)

# Unpack the Shipping Box

Verify that the following items are included:

1. Above Deck Unit (ADU)
2. ADU Mounting Kit
3. Below Deck Unit (BDU) with Rack Mount Kit
4. AC to 24VDC Power Supply
5. US/EU IEC Power Cable
6. Screw Terminal Block, 2 position (2)
7. RJ-45 Headers (RS-232 terminals) (6) (for solid/stranded core cables)
8. GPS Antenna
9. RJ-45 Feed-through Connector Assembly
10. Iridium Antenna with Mounting Kit + Optional remote mounting bracket
11. 2-ft Antenna Cable
12. ADU to BDU Communications cable, Multi RJ-45 to DB9

# Prepare Cabling

The connection between the ADU and BDU will require:

* Two (2) standard Ethernet CAT5 cables
* One (1) 2-conductor cable, 18 AWG (1.2mm) to 14 AWG (2.0mm)

These cables can be run as a bundle between the mounting locations of the ADU and BDU.

It is **strongly recommended** that each wire be properly marked for Iridium, GPS, power positive, and power negative. Incorrect Iridium/GPS wiring will prevent the unit from operating. Incorrect power wiring may damage the system.

The maximum wiring distance between the ADU and BDU is 500 ft (150 m).

> Six RJ-45 plugs are included in the kit for use with the ADU ↔ BDU cabling (if needed).
If these plugs are missing or exhausted, be sure to use the correct plugs for your cable. Solid core Ethernet cables should use solid core terminals, while stranded core cables should use stranded core terminals. The included plugs are designed to work with both types of cables.

The connection between the BDU and Uplogix appliance will require:

* ADU to BDU Communications cable, Multi RJ-45 to DB9 (included)
* 12"/CAT5e cable with BLUE boot <--> Serial port on the Uplogix appliance
* 36"/CAT5e cable with BLUE boot <--> RS232: GPS port on BDU
* 36"/CAT5e cable with BLACK boot <--> RS232: Local port on BDU

# Prepare the Above Deck Unit (ADU)

To open the ADU, turn the latch counterclockwise.

## Install the SIM card

Slide the cover of the SIM holder in the direction of the arrow (marked on cover) to open. Lift the cover and slide the SIM card into the slots in the cover. Align the beveled end of the SIM card with the mark in the holder (see picture). Carefully close the cover. Make sure the SIM card is properly seated and slide the cover back to lock it in place.

![ADU Internal](https://uplogix.com/support/docs/img/6.1/leo/chassis.jpg)

## Attach Mounting Bracket

If you will be using the included ADU Mounting Kit, attach the mounting brackets to the ADU now. The kit contains two V-bolts and a packet of mounting screws.

## Close and Latch Lid for Transport to Install Location

> When closing the lid of the ADU, take care not to disturb the gasket that fits between the lid and the body of the chassis.

# Install the Above Deck Unit (ADU)

## Mount the ADU

The ADU should be mounted within reach of the previously run cables. Other requirements:

* The antenna on the ADU should have a clear line of sight in all directions, to include 2 degrees above horizon.
* The ADU should not be the highest point at the desired location. A lightning strike could result in severe damage to the ADU, BDU, and any attached equipment.
* If the ADU is mounted to a pole with the supplied mounting bracket, the pole diameter cannot exceed 1.75 in. (44 mm).

## Wire the ADU for Power

Turn latch counterclockwise on the ADU and open the lid.

Insert the power cable through the far-right gland and route the wire to the power connector in the lower right-hand corner of the ADU. You will need a small screwdriver to connect the wires to the power module. Be sure the (+) positive is attached to pin 1 (far left side)

![ADU Power Plug](https://uplogix.com/support/docs/img/6.1/leo/power-plug.jpg)

The ADU can be closed at this time and locked by turning the latch clockwise until it stops.

## Connect Iridium and GPS Ports

**RJ-45:** Dress each cable if needed for standard straight-through configuration.

Standard RJ-45 cables can be pushed through the weather-tight glands and screwed into the appropriate RJ-45 socket on the chassis (RS422 to the left and GPS to the right).

![ADU RJ-45 Connector](https://uplogix.com/support/docs/img/6.1/leo/rj45-connector.jpg)

![ADU Chassis Connectors](https://uplogix.com/support/docs/img/6.1/leo/connections.jpg)

## Close and Latch ADU Lid

> When closing the lid of the ADU, take care not to disturb the gasket that fits between the lid and the body of the chassis.

# Attach Antennas

The antenna kit contains:

* Iridium antenna
* 2 ft LMR-195 cable
* GPS antenna with fixed 10 ft cable
* Combined Mounting bracket + Optional Mounting Bracket

Connect the LMR-195 cable to the external side of the N-type connector at the bottom of the ADU.

![ADU Chassis Connectors](https://uplogix.com/support/docs/img/6.1/leo/chassis-connectors.jpg)

Connect the LMR-195 cable to the Iridium antenna.

![ADU Antenna Assembly](https://uplogix.com/support/docs/img/6.1/leo/antenna-assembly-1.jpg)

Mount the antenna in the desired location. Use the circled holes in the below picture to attach the antenna to the mounting bracket with the screws provided.

![Antenna Holes](https://uplogix.com/support/docs/img/6.1/leo/antenna.jpg)

Unscrew the bottom cap of the GPS antenna and thread the wire through the top of the mounting bracket. Screw the cap back on and mount in desired location.

![ADU Assembled](https://uplogix.com/support/docs/img/6.1/leo/antenna-assembly-2.jpg)

**OPTIONAL:** Iridium Antenna Mount is included for remote mounting (includes V-bolts).

![Iridium Antenna Mount](https://uplogix.com/support/docs/img/6.1/leo/optional-mounting-brackets.jpg)

# Install the Below Deck Unit

![](https://uplogix.com/support/docs/img/6.1/leo/bdu-diagram.png)

> The BDU cannot be installed in a Local Manager expansion bay.

The left side of the BDU (marked RS232) connects to the Uplogix appliance.

The right side of the BDU (marked RS422) connects to the Above Deck Unit (ADU).

## Connect BDU to ADU

Locate the cable run from the ADU and dress the two serial cables with RJ-45 headers, using a straight-through configuration (if pre-dressed RJ-45 cables were not used).

Connect the Iridium cable to the port marked Remote.

Connect the GPS cable to the port marked GPS.

Strip the power cable and install it into the DC power header. A small screwdriver is required for this step.

Attach the DC power header to the power module (center right, marked + -).

> Observe correct polarity when wiring from the BDU to ADU. Incorrect wiring may cause severe damage to the ADU.

## Connect BDU to Local Manager

Connect the DB9 connector to the RS232 modem on the Uplogix appliance.

Connect the 12"/CAT5e cable with BLUE boot to the Uplogix appliance serial port.

Connect the 36"/CAT5e cable with BLUE boot to the GPS port on the BDU.

Connect the 36"/CAT5e cable with BLACK boot to the local port on the BDU.

## Connect BDU to Power

Use the included power supply and power cord to connect the BDU’s 24VDC power port to an electrical outlet. If power is configured correctly, the activity and traffic LEDs on the BDU will light up.

## Testing Iridium

Log into the Local Manager and navigate to the modem resource. By default, the modem has no configuration. Use the **terminal** command to open a session with the modem. Run ATZ and ati4. You should receive OK and Iridium in response.

```
[admin@UplogixLM]# modem
Iridium

[admin@UplogixLM (modem)]# t 
Press ~[ENTER] to exit Connecting ...
Console session started.

ATZ
ok

ati4
IRIDIUM
```

The output of **show serial** will show CTS and DSR as FALSE. This is normal for this system.

## Testing GPS

Navigate to the port that the GPS is connected to. Use the **config serial** command to set the baud rate of this port to 4800 (default for Garmin GPS).

Then, use the **terminal** command to open a session with the GPS receiver. You will not be able to enter any commands, but you should see NMEA traffic coming across the port. If there is no data or if the characters are garbled, try adjusting the baud rate or swap in another cable.

# Installation Complete

To continue with software configuration, see [LEO-I Kit Software Configuration](/docs/6.1/leo-kit-user-guide/local-manager-configuration/port-configuration)