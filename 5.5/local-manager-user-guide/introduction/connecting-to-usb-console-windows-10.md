<!-- 5.4 -->
[![1](http://uplogix.com/support/docs/img/Support-Doc-Site-Banner2.png)](http://uplogix.com "Uplogix.com")

# Overview

This document details how to open a USB console connection to an Uplogix Local Manager using a computer running Windows 10.

First, connect a USB console cable from your Windows 10 machine to the Local Manager mini-USB port.

## Locate the correct COM port

Right click on the Windows Start Icon and select "Device Manager."

![1](http://uplogix.com/support/docs/img/lm-user-guide/Windows10USB-Start.png)

Open the "Ports (COM & LPT)" Section.

![3](http://uplogix.com/support/docs/img/lm-user-guide/Windows10USB-Photo3.png)

Locate the "PI USB to Serial" and note which COM port it is using.

## Open a console session

Using PuTTY or other terminal emulator, select "Serial" as the connection type and change the "Serial line" to match the COM port noted earlier. The serial console speed is typically 9600.   

![4](http://uplogix.com/support/docs/img/lm-user-guide/Windows10USB-Photo4.png)

Click "Open" to connect to the console.



