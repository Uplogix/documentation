# Overview
The Uplogix LM83X Local Manager supports an LCD screen and keypad through an optional expansion card. The keypad can be used to configure the Local Manager without the need for a workstation. After configuration, the LCD screen displays system messages during boot and status information during normal operation.
# Using the keypad
The keypad consists of four arrow buttons, an Enter button (located in the center), and a Back button. The left and right arrow keys move the cursor left and right, respectively. The up and down arrow keys change numerical values.

![Uplogix LM83X LCD](https://uplogix.com/support/docs/img/6.0/lm83x-lcd.png)

When the Local Manager is powered on, press the Enter key in the center of the keypad to display the menu. Press the Back key below the left arrow key to exit the menu and resume scrolling status information.

The menu functions include:

## Configure

The Configure menu allows configuration of basic network and system settings. These settings include:

* IP Addressing - set the IP address, subnet mask, and default gateway 
* Control Center - set the IP address of your Uplogix Control Center
* Pulse IP - set the IP address of your Pulse server

## Restart

Restarts the Local Manager. Equivalent to the **restart** command
 
## Shutdown

Powers off the Local Manager. Equivalent to the **shutdown** command

## Update

Initiates a system upgrade from a USB flash drive. This option is available only if a USB flash drive is connected to the Local Manager. Equivalent to the **config update usb** command.

## Factory reset (hidden below two blank lines)

Restores the Local Manager to its initial state. Equivalent to the **config reinstall** command.

# Viewing Status Information
During normal operation, the LCD screen will cycle through various messages, including:

* Software Version
* Uplogix Status (Good, Out-of-Band, Upgrading, Alarms Exist, etc.)
* IP Address
* Control Center IP Address
* Pulse Server IP Address
* Port Information (hostname or description)

During the boot process, the LCD screen will display system messages.

In the event of a software or hardware error, the LCD screen may display the Uplogix logo or the Local Manager's serial number.