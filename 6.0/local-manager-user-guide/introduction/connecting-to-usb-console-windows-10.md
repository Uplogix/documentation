# Overview
This document describes connecting an Uplogix Local Manager to a Windows 10 computer using the USB console port.

# Locating the USB Console Port

## Uplogix LM80/LM83X

The USB console port on the LM83X is a USB-C port located in the Console stack to the left of the fixed serial ports.

**Note:** The USB A-Type port cannot be used to connect the Local Manager to a computer.

![](https://uplogix.com/support/docs/img/6.0/uplogix_lm83x_usb_console_port.png)

## Uplogix 500/5000

The USB console port on the 500/5000 is a Mini-USB port located to the right of the fixed ports.

**Note:** The USB A-Type ports cannot be used to connect the Local Manager to a computer.

![](https://uplogix.com/support/docs/img/6.0/uplogix_5000_usb_console_port.png)

# Connect the USB cable
Connect the Local Manager to a Windows 10 computer using the appropriate cable.
# Locate the correct COM port

Right click on the Windows Start Icon and select "Device Manager."

![1](http://uplogix.com/support/docs/img/lm-user-guide/Windows10USB-Start.png)

Open the "Ports (COM & LPT)" Section.

![3](http://uplogix.com/support/docs/img/lm-user-guide/Windows10USB-Photo3.png)

Locate the "PI USB to Serial" and note which COM port it is using.

## Open a console session

Using PuTTY or other terminal emulator, select "Serial" as the connection type and change the "Serial line" to match the COM port noted earlier. The serial console speed is typically 9600.   

![4](http://uplogix.com/support/docs/img/lm-user-guide/Windows10USB-Photo4.png)

Click "Open" to connect to the console.



