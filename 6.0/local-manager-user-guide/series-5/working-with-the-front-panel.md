# Overview
The Uplogix 5000 Local Manager has an LCD screen and keypad built into the chassis. The keypad can be used to configure the Local Manager without the need for a workstation. After configuration, the LCD screen displays system messages during boot and status information during normal operation.
# Using the keypad
The keypad consists of four arrow buttons, and enter button (located in the center), and a back button. The left and right arrow keys move the cursor left and right, respectively. The up and down arrow keys change numerical values.

![Uplogix 5x Keypad](http://uplogix.com/support/docs/img/lm-user-guide/image015.png)

The keypad located on the front panel provides up, down, left, and right keys (labeled with arrows) as well as enter/power (i.e., the middle key) and back keys. The left and right arrow keys move the cursor left and right, respectively. The up and down arrow keys change numerical values.

Press the Enter/Power key in the center of the keypad to power the Local Manager on when it is powered off. When the Local Manager is powered on, press the Enter/Power key in the center of the keypad to display the menu. The menu functions include:

**Configure**

Covers the steps needed to work with the Local Manager via an SSH session. Equivalent to the following commands: **config system ip**, **config system management**, and **config system pulse**.

**Restart**

Reboots the Local Manager. Equivalent to the **restart** command
 
**Shutdown**

Powers off the Local Manager. Equivalent to the **shutdown** command

**Update**

Upgrade the software from the USB flash drive. This option is available only if a USB flash drive is connected to the Local Manager. Equivalent to the **config update usb** command.

**Factory reset**

Restores the Local Manager to its initial state. Equivalent to the **config reinstall** command.

Press the Back key below the left arrow key to exit the menu and resume scrolling status information.

# Front Panel Operations

In most cases, the command line provides the functionality needed to work with the Local Manager. The front panel allows basic configuration, power, and reset operations.

## Uplogix 500 Power and Restart Operations

| To do this: | Check to be sure that: | Take this action: | The process is complete when: |
| -- | -- | -- | -- |
| Power on | All lights are off | Plug in the power supply and then press the power button on the front panel. |	 The system status light will slowly blink while the Local Manager boots and will become solid green when the boot process completes. |
| Power on | The system status light is off and the power supply light is on (amber) |	Press the power button on the front panel. | The system status light will slowly blink while the Local Manager boots and will become solid green when the boot process completes. |	
| Restart | The system health light is on and not blinking | A restart is only supported from the CLI or UCC for this platform. To manually restart this platform, follow the instructions in this table to power off and then power on the Local Manager. |
| Power off	| The system status light is on and not blinking | Press and release power button to initiate a graceful shutdown of the system. The system status light will blink as the unit shuts itself down. | The system status light is off and the power indicator is amber. |

## Uplogix 5000 Power and Restart Operations
| To do this: | Check to be sure that: | Take this action: | The process is complete when: |
| -- | -- | -- | -- |
| Power on | All lights are off | Plug in one or both power supplies. A dimly lit keypad and dark LCD indicates power is applied but that the LM is powered down. Next, press the center button on the keypad to power the LM on. | The LCD is scrolling Local Manager information and device status |
| Power on | Keypad is dimly lit but the LCD is dark/off. | Press the center button on the keypad to power the LM on. | The LCD is scrolling Local Manager information and device status |
| Restart | The LCD is scrolling Local Manager information and device status | Press the center button on the keypad. Press the down arrow button to navigate to the Restart menu item. Press the center button to select Restart. | The LCD is scrolling Local Manager information and device status |
| Power off | The LCD is scrolling Local Manager information and device status | Press the center button on the keypad. Press the down arrow button to navigate to the Shutdown menu item. Press the center button to select Shutdown. | The keypad is dimly lit and the LCD is dark/off. |