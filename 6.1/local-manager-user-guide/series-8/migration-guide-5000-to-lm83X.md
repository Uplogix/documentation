# Overview
This document describes the process for migrating an installation from an Uplogix 5000 to an Uplogix LM83X. While the two products share the same software and much of the same functionality, there are a few differences to be aware of.

# Fixed Ports

Previously, the six fixed, built-in ports on the Uplogix 5000 were connected to an LCD and keypad and were located on the right side of the chassis.

![Uplogix 5000 Local Manager Slot 1 Highlighted](https://uplogix.com/support/docs/img/6.0/uplogix_lm5000_slot1.png)

In the LM83X, the fixed ports have been separated from the LCD and Keypad and relocated to the left side of the chassis. The number of ports has been increased to 8.

![Uplogix LM83X Local Manager Slot 1 Highlighted](https://uplogix.com/support/docs/img/6.0/uplogix_lm83x_slot1.png)
 
# Slot Count and Numbering
The number of expansion card slots has increased from 2 on the Uplogix 5000 to 3 on the LM83X. The relocated fixed ports are now Slot 1, and the remaining slots increment to the right.

On the Uplogix 5000, slots were numbered from right to left.

![Uplogix 5000 Local Manager Slot Numbers](https://uplogix.com/support/docs/img/6.0/uplogix_5000_slot_numbers.png)

On the Uplogix LM83X, slots are now numbered from left to right.

![Uplogix LM83X Local Manager Slot Numbers](https://uplogix.com/support/docs/img/6.0/uplogix_lm83x_slot_numbers.png)

For reference, slots numbers are visible through holes in the expansion cards below the left thumbscrew.

![Uplogix LM83X Slot Number Pass-throughs](https://uplogix.com/support/docs/img/6.0/uplogix_lm83x_chassis_slot_numbers.png) 
# LCD and Keypad
The LCD and Keypad have been redesigned as an expansion card for the LM83X. It can be installed in any open expansion slot or left out altogether. Uplogix recommends installing the LCD and Keypad card in the right-most bay for consistent slot numbering in the software.
# Expansion Cards
<div class='warning' />Uplogix 5000 expansion cards are not compatible with LM83X and cannot be used interchangeably.</div>

The LM83X supports the following expansion cards:

* 8-port Serial Expansion Module
* 16-port Serial Expansion Module (serial fan-out cables ARE compatible between systems)
* 8-port Ethernet Expansion Module
* LCD and Keypad Module

**Note:** Unlike the Uplogix 5000, the LM83X does not provide a 4-port Serial Expansion Module.
# Migration Process â€“ Without a Control Center
For a smooth transition from an Uplogix 5000 to an LM83X, ensure the following:

* LM83X should contain the same types of expansion cards
* LM83X expansion cards should be in the same logical order

For example, if there is a 16-port Serial Expansion Module is slot 2 on the Uplogix 5000, a 16-port Serial Expansion Module should be installed in slot 2 of the LM83X, despite it being a different physical position due to the change in slot numbering.

Perform the following steps:

1. Export the configuration of the Uplogix 5000 with the **config export** command. 
2. Label all cables with slot and port numbers so they can be reconnected to the LM83X.
3. Shut down the Uplogix 5000 and remove it from the rack.
4. Install the LM83X in its place.
5. Reconnect all cables, including Ethernet, fiber, POTS lines, and cellular antennas.
6. Assign an IP address, subnet mask, and default gateway if DHCP is not available.
7. Import the configuration onto the LM83X using the **config import** command.
8. Verify configuration.

# Migration Process â€“ With a Control Center
For a smooth transition from an Uplogix 5000 to an LM83X, ensure the following:

* LM83X should contain the same types of expansion cards
* LM83X expansion cards should be in the same logical order

For example, if there is a 16-port Serial Expansion Module is slot 2 on the Uplogix 5000, a 16-port Serial Expansion Module should be installed in slot 2 of the LM83X, despite it being a different physical position due to the change in slot numbering.

Perform the following steps:

1. Label all cables with slot and port numbers so they can be reconnected to the LM83X.
2. Shut down the Uplogix 5000 and remove it from the rack.
3. Install the LM83X in its place.
4. Reconnect all cables, including Ethernet, fiber, POTS lines, and cellular antennas.
5. Assign an IP address, subnet mask, and default gateway if DHCP is not available. 
6. Log into the Control Center and locate the 5000 to be replaced.
7. Click the Replace button. (See: [Replacing a Local Manager](https://uplogix.com/docs/control-center-user-guide/managing-local-managers/replacing-a-local-manager))
8. Select the new LM83X from the dropdown list.
9. Verify configuration.

During the replace, the Local Manager will attempt to map the 5000â€™s ports to the LM83X.

* Since the 5000 does not have a port 1/7 or 1/8, those ports will remain in native mode on the LM83X.
* If a corresponding slot on the LM83X is not available, the slot and ports will be ignored.
* If the corresponding slot on the LM83X has fewer ports (8 vs 16), the extra ports will be ignored.
* If the corresponding slot on the LM83X has more ports, the extra ports will remain in native mode.
* Virtual Slot 4 on the 5000 will be renumbered to Virtual Slot 5 on the LM83X.

