# Overview

This document describes how to use the Uplogix Local Manager to access and control a C-Com antenna controller.

## Required Privileges

* **terminal** - When used with the binary option, opens and forwards a terminal session

## Other Requirements

* Use of this feature requires C-Com's iNetVu Mobile software and virtual serial port software. Uplogix has tested and recommends Tactical SW's Serial/IP Redirector v4.9.1 or later. Other virtual serial port software may not support this application.
* C-Com software version 7.2.6 or greater is required.

# Forwarding Setup

There are two methods to connect to the C-Com antenna controller via an in-band connection or an out-of-band connection. Both connections use the workstation's 127.0.0.1 loopback interface. An available local port is presented via the Control Center applet (CLI applet when in-band and Dial applet when out-of-band) and configured in the virtual serial port program for streaming to iNetVu Mobile. 

> The **config init** command is not required as there is no advanced driver for C-Com Antennas. The default *native* will be used instead.

To begin, navigate to the port with the C-Com connected using the port command. Then enter into a terminal session with the **terminal binary** command as shown in the example below: 

```
[admin@UplogixLM]# port 1/2
native
C-Com 7000

[admin@UplogixLM (port1/2)] terminal binary

Press ~[ENTER] to exit.
Connecting ...
Console session started. Press ~[ENTER] to exit.
~~@ï‚‚Â½ï‚‰' Â°Â·   1~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~â”~~@ï‚‚Â½ï‚‰' Â°Â·   1~~@ï‚‚Â½ï‚‰' Â°Â·   ~~@ï‚‚Â½ï‚‰' Â°Â·   1~~@ï‚‚Â½ï‚‰' Â°Â·   /~~@ï‚‚Â½ï‚‰' Â°Â·   /~~@ï‚‚Â½ï‚‰' Â°Â·    .
```

Once the terminal session has started, you will need to disable the Uplogix terminal commands using the **~\** command as in the example below:

```
Once you disable ~ commands, you will not be able to use ~[ENTER] to end your terminal session. Your current terminal session will continue until either the device pass through timeout is reached or you disconnect.

Disable all ~ commands? (y/n) [n]: y
All ~ commands are disabled.
```

Once the terminal session has started, initiate a forward to iNetVu. On the Terminal menu of the CLI applet, select Forward. Enter an open port number above 1024 that matches the port number you assigned in the virtual serial port program. Click the apply button to establish this port setting. The green colored background of the port number indicates the port is available. A red colored background indicates the port is not available and another port should be selected. Now all interaction with the C-Com antenna controller M&C port is being forwarded to the workstation's loopback address (127.0.0.1), which is in turn directed to a virtual serial port.

![Forward Settings](http://uplogix.com/support/docs/img/configuration-guides/c-com1.png) 


# Virtual Serial Port Setup

Launch your virtual serial port program and create a COM port that is configured to the workstation's loopback interface at 127.0.0.1 on an open port. Be sure to match the port configured in the forward settings. In this example, 9001 has been selected.

![Serial/IP Control Panel](http://uplogix.com/support/docs/img/configuration-guides/c-com2.png) 
  
Configure the program to a normal telnet connection without special options for text padding or raw-mode modifications. All incoming connections will be requested/declared as "binary telnet mode" connections.

![Serial/IP Advanced Settings](http://uplogix.com/support/docs/img/configuration-guides/c-com3.png)  

# Running iNetVu 

Next, launch the iNetVu Mobile software. When the software program starts, it will declare which COM port it is using for communications. You can check this setting by right clicking on the screen and selecting the Configuration menu.

![Forward Settings](http://uplogix.com/support/docs/img/configuration-guides/c-com4.png) 

Ensure the COM port in the virtual serial port software matches the declared COM port. Update the virtual serial port configuration if necessary. In this example the COM port is COM3. 
Data is now streaming through the virtual serial port and populating the iNetVu program. If your workstation has speakers, you may hear an audible dinging sound.

![iNetVu Advanced Controls](http://uplogix.com/support/docs/img/configuration-guides/c-com5.png) 

As iNetVu Mobile queries the C-Com controller, the text-window of the Applet may visually appear to freeze or stick after displaying random characters. This is expected behavior that will not impact your session with the C-Com controller.

![SSH Session](http://uplogix.com/support/docs/img/configuration-guides/c-com6.png)

To exit the forwarded session, simply close the window or wait for the port to time out due to lack of activity. You may want to consider altering the timeout from the default value to 120 seconds using the **configure settings** command.

#Troubleshooting

## Connection Issues

There are two indicators that the forwarded connection is not correctly populating data. When the iNetVu Mobile program launches, the software will indicate that it is "reading all parameters". If the status message does not quickly change to "all parameters read" you may need to reset your virtual serial port connection by closing and restarting the iNetVu Mobile software. If after closing and re-opening the iNetVu Mobile software, the error persists, reconfirm your configuration settings by ensuring you have used the terminal binary command, turned off tilde commands with the  ~\ command, and checked your virtual serial software and connection settings. You should see high ASCII characters scrolling across the terminal screen - if not, verify that no device is connected to the USB port on the C-Com device. For the case where there was a USB device plugged in, remove the device and reboot the C-Com device.

The second indicator that the software is having difficulty capturing the information to populate the program is a "CRC error" message. To resolve this issue, close and restart the iNetVu Mobile software.  

## Start Up Order

It is important to observe the startup order identified in this guide. You must terminal into the C-Com antenna controller prior to attempting to start iNetVu. If you start the iNetVu program before issuing the Terminal Binary command, the flood of characters across the console will prevent you from entering the command.

## Stalled Connection

During initialization of the connection, the terminal session may reach an idle timeout while you are preparing the iNetVu software. Characters in the terminal session will cease scrolling across the console and it appears the antenna controller is not communicating with the iNetVu software. To remedy this situation, press enter in terminal window and you should see binary characters begin scrolling across the terminal.