# Overview
This guide describes the procedures for installing, cabling, and provisioning Uplogix Local Managers.

This guide applies to the following models:

* Uplogix LM83X
* Uplogix LM80

**Please read the [Uplogix Safety Summary](http://uplogix.com/docs/local-manager-user-guide/reference/safety-summary) before proceeding with installation.**

# Site Requirements

Ensure that the power source meets the following requirements:

* Provides appropriate power (AC or DC) as required by the Local Manager
* Provides overload protection
* Is connected to earth ground

<div class='danger'>The power source must meet all requirements to ensure safe and reliable operation.</div>

Ensure the installation site ambient temperature does not exceed 113F (45C) or fall below 32F (0C).

<div class='warning'>The unit will overheat if the sites does not meet these requirements.</div>

# Optional equipment

The following optional equipment is available for Uplogix Local Managers.

* v.92 modem
* DB-9 (RS-232) serial module
* Cellular modem
* SFP (fiber) module

# Install a v.92 modem

Follow these steps if a v.92 modem is not already installed in the option slot.

1.	Power off the Local Manager.
2.	Remove the option slot cover, align the modem carrier card with the internal rails, and slide the modem into place.
3.	Replace the screws.
4.	Connect a POTS telephone line to the RJ-11 jack on the modem
5.	Power on the Local Manager.

![v92 modem diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image007.png)

# Install a DB-9 serial module

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

# Install a GPRS cellular modem

Follow these steps to install the GPRS cellular modem:

1.	Power off the Local Manager.
2.	Install an activated SIM card on the modem.
3.	Remove the option slot cover, align the modem carrier card with the internal rails, and slide the modem into place.
4.	Feed wire into the option slot compartment, align modem cover plate with the option slot screw holes, and replace the screws.
5.	Install antenna.
6.	Power on the Local Manager.

![GPRS cellular modem diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image008.png)

# Install a CDMA cellular modem

Follow these steps to install the CDMA cellular modem:

1.	Power off the Local Manager.
2.	Note the Electronic Serial Number (ESN) on the modem, as this will be needed in order to activate the modem on your carrierâ€™s network.
3.	Remove the option slot cover, align the modem carrier card with the internal rails, and slide the modem into place.
4.	Feed wire into the option slot compartment, align modem cover plate with the option slot screw holes, and replace the screws.
5.	Install antenna.
6.	Power on the Local Manager.

![CDMA cellular modem diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image008.png)

# Install an SFP module
<div class='info'>An SFP module comes built-in on LM80/LM83X hardware. These instructions are for installing an additional SFP module.</div>

Follow these steps to install the SFP module:

1.	Power off the Local Manager
2.	Remove the option slot cover, align the carrier card with the internal rails, and slide the module into place.
3.	Replace the screws.
4.	Install either a 1000Base SX (GLC-SX-MM) SFP or the 1000Base LX/LH (GLC-LH-SM) SFP for fiber connectivity. Both the 1000Base SX (GLC-SX-MM) SFP and the 1000Base LX/LH (GLC-LH-SM) SFP are customer-provided equipment. 

<div class='info'>SFP modules are hot swappable, but the SFP carrier option card is not hot swappable.</div>

![SFP module diagram](http://uplogix.com/support/docs/img/installing-a-local-manager/image010.png)

# Install a temperature and humidity sensor

Environmental monitoring is available via a USB-connected temperature and humidity sensor.

Follow these steps to connect the sensor. Note the Local Manager does not need to be powered down for installation of this sensor.

1.	Plug the sensor into one of the two USB connections on the Local Manager.
2.	Place sensor collection end in the area you wish to collect environmental information, ideally not near a fan or on hot equipment.

It may take up to 10 minutes for the sensor to normalize to the environmental temperature and begin reporting consistent data. 

# Install expansion cards

Please see the following documents for more information about expansion cards:

* [Expansion Cards](https://uplogix.com/docs/local-manager-user-guide/series-8/expansion-cards)

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

# Install chassis in rack

Uplogix Local Managers are designed for standard 19-inch telco racks.

The Uplogix 500 ships with rubber standoffs for desktop use.

## Uplogix LM83X

To mount the Local Manager in a rack:

1. Use the included screws to attach the mounting brackets.
![Uplogix 5000 Rack Brackets](http://uplogix.com/support/docs/img/installing-a-local-manager/image025.png)
2. Mount the Local Manager in the rack

## Uplogix LM80

To mount the Local Manager with the optional center-mount kit:

1.	Attach the mounting brackets.
2.	Mount the Local Manager in the rack.
![Uplogix 500 Center Mount](http://uplogix.com/support/docs/img/installing-a-local-manager/image012.png)

# Connect to power

Before connecting the Local Manager to power, ensure all [site requirements](#site-requirements) are met.

Connect the power cord to the Local Manager. Use either the provided power cord or one that is suitable for your location. The Uplogix Local Manager uses a power cord with a standard IEC-320-C13 female cord end.

![A Power Cord](http://uplogix.com/support/docs/img/lm-user-guide/plug.png)
 
Connect the power cord to a power outlet. A dimly lit keypad and dark display (if installed) indicates that the unit has power applied. Power the unit on by pressing the middle keypad button. The display on the front panel will illuminate and display progress messages as the device boots. At the end of the boot sequence, it displays the message **Uplogix status good**.

# Installation complete

You are now ready to complete the initial setup of the Uplogix Local Manager.