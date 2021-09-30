<!-- 5.5 -->

The Uplogix LEO-I kit (Revision 3) can be used with the Uplogix 500/5000/LM80/LM83X Local Managers.

## Required Equipment

### SIM Card

A valid and active SIM card is required for access to the Iridium satellite network. Contact your Service Provider if you do not have a SIM card.

### Uplogix Appliance
 
Uplogix 500/5000/LM80/LM83X models have modem option slots on the front of the chassis and must have an RS-232 module installed.

![u5k RS-232 Module](http://uplogix.com/support/docs/img/hawk/image005.png)
 
## Unpack the shipping box

Verify that the following items are included:

* Above Deck Unit (ADU)
* ADU Mounting Kit
* Below Deck Unit (BDU) with Rack Mount kit
* AC to 24VDC Power Supply
* US/EU IEC Power Cable
* Screw Terminal Block, 2 position (2)
* RJ-45 Headers (RS-232 Terminals) (6)
	* These headers are designed to work with both solid and stranded core Ethernet cables.
* GPS Antenna
* RJ-45 Feed-through Connector Assembly
* Iridium Antenna with Mounting Kit
* 10-ft Antenna Cable
* ADU to BDU Communications cable, Multi RJ-45 to DB9



## Prepare Cabling

The connection between the ADU and BDU will require:

* Two (2) standard Ethernet CAT5 cables
* One (1) 2 conductor cable, 18 AWG (1.2mm) to 14 AWG (2.0mm)

These cables can be run as a bundle between the mounting locations of the ADU and BDU.

It is **strongly recommended** that each wire be properly marked for Iridium, GPS, power positive, and power negative. Incorrect Iridium/GPS wiring will prevent the unit from operating. Incorrect power wiring may damage the system.

The maximum wiring distance between the ADU and BDU is 500 ft (150 m).

> Six RJ-45 plugs are included in the kit for use with the ADU â†” BDU cabling (if needed). If these plugs are missing or exhausted, be sure to use the correct plugs for your cable. Solid core Ethernet cables should use solid core terminals, while stranded core cables should use stranded core terminals. The included plugs are designed to work with both types of cables.

The connection between the BDU and Uplogix appliance will require:

* ADU to BDU Communications cable, Mutlti RJ-45 to DB9 (included)
	* **12"**/CAT5e cable with <span style="color:blue">**BLUE**</span> boot <--> Serial port on the Uplogix appliance
	* **36"**/CAT5e cable with <span style="color:blue">**BLUE**</span> boot <--> RS232: GPS port on BDU
	* **36"**/CAT5e cable with <span style="color:black">**BLACK**</span> boot <--> RS232: Local port on BDU

## Prepare the Above Deck Unit (ADU)

To open the ADU, turn latch counterclockwise.

### 1. Install the SIM card

Slide the cover of the SIM holder in the direction of the arrow (marked on cover) to open. Lift the cover and slide the SIM card into the slots in the cover. Align the beveled end of the SIM card with the mark in the holder (see picture). Carefully close the cover. Make sure the SIM card is properly seated and slide the cover back to lock it in place.

![Above Deck Unit with RJ-45 Wiring](http://uplogix.com/support/docs/img/hawk/Sim-Card-View.jpg)

### 2. Attach mounting bracket

If you will be using the included ADU Mounting Kit, attach the mounting brackets to the ADU now. The kit contains two U-bolts and a packet of mounting screws. 



### 3. Replace lid for transport to install location

> When closing the lid of the ADU, take care not to disturb the gasket that fits between the lid and the body of the chassis.

## Install the Above Deck Unit (ADU)

### 1. Mount the ADU at the desired location

The ADU should be mounted within reach of the previously run cables. Other requirements:

* The antenna on the ADU should have a clear line of sight in all directions, to include 2 degrees above horizon. 
* The ADU should not be the highest point at the desired location. A lightning strike could result in severe damage to the ADU, BDU, and any attached equipment.
* If the ADU is mounted to a pole with the supplied mounting bracket, the pole diameter cannot exceed 1.75 in. (44 mm).
 
### 2. Wire the ADU for power

Turn latch counterclockwise on the ADU and open the lid.

Insert the power cable through the far-right gland and route the wire to the power connector in the lower right-hand corner of the ADU. You will need a small screwdriver to connect the wires to the power module. Be sure the (+) positive is attached to pin 1 (far left side).

![Above Deck Unit with RJ-45 Wiring](http://uplogix.com/support/docs/img/hawk/ADU-Power-Wire.jpg)


### 3. Connect Iridium and GPS ports

**RJ-45**: Dress each cable (if needed) for standard straight-through configuration. Standard RJ-45 cables can be pushed through the weather-tight glands and screwed into the appropriate RJ-45 socket on the chassis (RS422 to the left and GPS to the right).

![Connect Iridium and GPS ports](http://uplogix.com/support/docs/img/hawk/RJ-45-Cable-Dressed.jpg)

![Connect Iridium and GPS ports](http://uplogix.com/support/docs/img/hawk/RS422-GPS-Connection.jpg)


### 4. Close and secure ADU

The ADU can be closed at this time and locked by turning the latch clockwise until it stops.

> When closing the lid of the ADU, take care not to disturb the gasket that fits between the lid and the body of the chassis.

## Install the Below Deck Unit (BDU)

![Below Deck Unit](http://uplogix.com/support/docs/img/hawk/image006.png)

> **NOTE:** The BDU cannot be installed in an Uplogix 5000 expansion bay.

The left side of the BDU (marked **RS232**) connects to the Uplogix appliance.

The right side of the BDU (marked **RS422**) connects to the Above Deck Unit (ADU).

### 1. Connect BDU to the ADU

* Locate the cable run from the ADU and dress the two serial cables with RJ-45 headers, using a straight-through configuration (if pre-dressed RJ-45 cables were not used).
* Connect the Iridium cable to the port marked *Remote* 
* Connect the GPS cable to the port marked GPS.
* Strip the power cable and install it into the DC power header. A small screwdriver is required for this step.
* Attach the DC power header to the power module (center right, marked + -).

> Observe correct polarity when wiring power from the BDU to ADU. Incorrect wiring may cause severe damage to the ADU.

### 2. Connect BDU to Uplogix appliance

Use the ADU to BDU Communications cable to connect the Local RS-232 ports of the BDU to the Uplogix appliance.
 
* Connect the DB9 connector to the RS232 modem on the Uplogix appliance.
* Connect the 12"/CAT5e cable with <span style="color:blue">**BLUE**</span> boot to the Uplogix appliance serial port.
* Connect the 36"/CAT5e cable with <span style="color:blue">**BLUE**</span> boot to the GPS 
* Connect the 36"/CAT5e cable with <span style="color:black">**BLACK**</span> boot to the local port on the BDU.

### 3. Connect BDU to power

Use the included power supply and power cord to connect the BDU's 24VDC power port to an electrical outlet. If power is configured correctly, the activity and traffic LEDs on the BDU will light up.

