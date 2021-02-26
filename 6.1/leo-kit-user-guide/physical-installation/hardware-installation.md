The Uplogix LEO-I kit can be used with Local Managers equipped with an RS-232 module.

## Required Equipment

### SIM Card

A valid and active SIM card is required for access to the Iridium satellite network. Contact your Service Provider if you do not have a SIM card.

The SIM card should be provisioned for Data. If you will be using SMS-initiated PPP, the SIM card will need to be provisioned for Voice as well.

### Uplogix Local Manager

An RS-232 module must be installed in the modem option slot of the Uplogix Local Manager as seen on the Uplogix 3200 model below.

![u3200 Rear Panel](http://uplogix.com/support/docs/img/hawk/image004.png)
 
Uplogix 500/5000/LM80/LM83X models have modem option slots on the front of the chassis and must have an RS-232 module installed.

![u5k RS-232 Module](http://uplogix.com/support/docs/img/hawk/image005.png)
 
## Unpack the shipping box

Verify that the following items are included:

* Above Deck Unit (ADU)
* ADU Mounting Kit
* Below Deck Unit (BDU)
* DB-9 to RJ-45 Adapter (Labeled LEO-PA)
* AC to 24VDC Power Supply
* US/EU IEC Power Cable
* DC Power Connectors (2)
* RJ-45 Headers (RS-232 Terminals) (6)
	* These headers are designed to work with both solid and stranded core Ethernet cables.

## Prepare Cabling

The connection between the ADU and BDU will require:

* Two (2) standard Ethernet CAT5 cables, undressed (no RJ-45 connectors)
* One (1)  18 gage (1.2mm) to a maximum of 14 gage (2.0mm) power cable, undressed

These cables can be run as a bundle between the mounting locations of the ADU and BDU. The cables terminating at the ADU should not have connectors, as they will not be able to pass through the ADU gaskets with RJ-45 connectors attached.

It is **strongly recommended** that each wire be properly marked for Iridium, GPS, power positive, and power negative. Incorrect Iridium/GPS wiring will prevent the unit from operating. Incorrect power wiring may damage the system.

The maximum wiring distance between the ADU and BDU is 500 ft (150 m).

> Six RJ-45 plugs are included in the kit for use with the ADU â†” BDU cabling. If these plugs are missing or exhausted, be sure to use the correct plugs for your cable. Solid core Ethernet cables should use solid core terminals, while stranded core cables should use stranded core terminals. The included plugs are designed to work with both types of cables.

The connection between the BDU and Uplogix appliance will require:

* One (1) standard Ethernet CAT5 cable, straight-through (for Iridium)
* One (1) rolled Ethernet CAT5 cable (for GPS)
	* A rolled cable is **REQUIRED** for proper operation with the Uplogix 5000, 500 and 430 Local Managers. If you are using an Uplogix 3200, a straight-through cable can be substituted.â€ƒ

## Prepare the Above Deck Unit (ADU)

To open the ADU, remove the four screws located at each corner of the lid. 

### 1. Install the SIM card

Remove the cover to the SIM card compartment on the 9522B and install the SIM card. Ensure that the card is in the correct orientation.

### 2. Attach mounting bracket

If you will be using the included ADU Mounting Kit, attach the mounting brackets to the ADU now. The kit contains two U-bolts and a packet of mounting screws. 

On some models, the mounting brackets will already be attached to the ADU.

### 3. Install the remote antenna (OPTIONAL)

To install the optional remote antenna kit, see [Remote Antenna Kit](https://uplogix.com/docs/leo-kit-user-guide/physical-installation/remote-antenna-kit).

### 4. Replace lid for transport to install location

Secure at least 1 of the corner screws before moving the ADU to its final location.

> When closing the lid of the ADU, take care not to disturb the gasket that fits between the lid and the body of the chassis.

## Install the Above Deck Unit (ADU)

### 1. Mount the ADU at the desired location

The ADU should be mounted within reach of the previously run cables. Other requirements:

* The antenna on the ADU should have a clear line of sight in all directions, to include 2 degrees above horizon. 
* The ADU should not be the highest point at the desired location. A lightning strike could result in severe damage to the ADU, BDU, and any attached equipment.
* If the ADU is mounted to a pole with the supplied mounting bracket, the pole diameter cannot exceed 1.75 in. (44 mm).
 
### 2. Wire the ADU for power

Remove the corner screws of the ADU and open the lid.

Insert the power cable through the far-right gasket and route the wire to the power connector in the upper right-hand corner of the ADU. You will need a small screwdriver to connect the wires to the power module.

Leave the ADU open.

### 3. Connect Iridium and GPS ports

Thread the Iridium and GPS cables through their respective gaskets at the bottom of the ADU. Connect the cables to the PCB using the desired method. Ensure there are no tight bends in the cables by looping the cables inside the ADU. See the included photo for an example.

**RJ-45:** Dress each cable for standard straight-through configuration. Attach RJ-45 headers and connect to the Iridium and GPS ports on the PCB.

**Terminal Blocks:** Locate the green terminal blocks on the PCB. Consult the diagram included in this guide to identify the RS-422 9522B and GPS blocks. Each pin is labeled according to the 568-B wiring standard. Be sure to adjust for your wiring scheme if not using 568-B.

Strip the cable jacket of the CAT5 to the length of the terminal block. Strip individuals wires about a quarter inch. Insert wires into the terminal block, ensuring wire pairs remain twisted.

### 4. Close and secure ADU

Replace the lid on the ADU and fasten each corner screw tightly. 

> When closing the lid of the ADU, take care not to disturb the gasket that fits between the lid and the body of the chassis.

## Install the Below Deck Unit (BDU)

![Below Deck Unit](http://uplogix.com/support/docs/img/hawk/image006.png)

If you are connecting the BDU to an Uplogix 3200 with an available expansion bay, you can remove the BDU from its standalone chassis and install it in an empty bay. Move the thumbscrews on the BDU from their default positions to the center holes to secure the BDU to the 3200 chassis. Newer model BDUs come equipped with a single rack ear that can be used to rack mount the BDU.

> **NOTE:** The BDU cannot be installed in an Uplogix 5000 expansion bay.

The left side of the BDU (marked **RS232**) connects to the Uplogix appliance.

The right side of the BDU (marked **RS422**) connects to the Above Deck Unit (ADU).

### 1. Connect BDU to the ADU

* Locate the cable run from the ADU and dress the two serial cables with RJ-45 headers, using a straight-through configuration. 
* Connect the Iridium cable to the port marked Remote. 
* Connect the GPS cable to the port marked GPS.
* Strip the power cable and install it into the DC power header. A small screwdriver is required for this step.
* Attach the DC power header to the power module (center right, marked + -).

> Observe correct polarity when wiring power from the BDU to ADU. Incorrect wiring may cause severe damage to the ADU.

### 2. Connect BDU to Uplogix Local Manager

Use Ethernet cables to connect the Local RS-232 ports of the BDU to the Uplogix Local Manager.
 
**BDU RS-232 LOCAL â†” LEO-PA DB-9 ADAPTER â†” UPLOGIX RS-232 MODULE** â€“ Use a straight-through Ethernet cable to connect the Local port of the BDU to the LEO-PA adapter. Plug the adapter into the RS-232 module on the Uplogix appliance.

> Note that the LEO-PA adapter is **REQUIRED** for proper operation. If the LEO-PA adapter is missing, see the wiring diagram at the end of this document.

**BDU RS-232 GPS â†”UPLOGIX LOCAL MANAGER** â€“ Use a rolled (for example, a flat, blue Cisco console cable) Ethernet cable to connect the GPS port of the BDU to a free serial port on the Uplogix appliance. 

> A straight-through cable may be used with an Uplogix 3200 if the Local Manager serial portâ€™s null-modem setting is set to **YES** or **AUTO**.
> This connection is not required for proper operation of the LEO-I kit. However, a cable between the GPS ports on the BDU and ADU is still required.

### 3. Connect BDU to power

Use the included power supply and power cord to connect the BDUâ€™s 24VDC power port to an electrical outlet. If power is configured correctly, the activity and traffic LEDs on the BDU will light up.