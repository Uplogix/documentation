# Overview

The purpose of this document is to detail the installation and configuration of Intellian satellite Antenna Controller Units (ACU) for use with Uplogix Local Managers. 

# Supported Models

The Uplogix Local Management Software (LMS) version 4.4+ includes support for Intellian ACUs and Arbitrators including the V-Series models. 

# Physical Installation

Connect the RS-232 PC port on the Intellian ACU to the Uplogix Local Manager using a DB-9 to RJ-45 adapter and a standard Cat-5 cable. The pinout for the adapter is below:

| RJ-45 Pin | Color | DB-9 Pin
|-|-|
| 1	| Blue | 7
| 2	| Orange | 4
| 3	| Black | 3
| 4	| Green | 5
| 5	| Red	| 5
| 6	| Yellow | 2
| 7	| Brown | 6
| 8	| White | 8
 
![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image001.png)

![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image002.png)

# Configuring the ACU

The Intellian ACU uses the Uplogix Local Manager native driver. This driver will provide connectivity to the Intellian V-Series PC Controller application through Secure Shell (SSH) or Uplogix CLI applet to the Uplogix Local Manager.

Use a workstation to open a command line session with the Uplogix Local Manager.

Issue the **port** command to navigate to the port your Intellian ACU is connected to. In the example below it is attached to port 3 of slot 1.

```
[admin@UplogixLM]# port 1/3
native
[admin@UplogixLM (port 1/3)]#
```

Use the **config serial** command to change the serial speed from 9,600 to 19,200 (the default for the Intellian ACU).

```
[admin@UplogixLM (port 1/3)]# config serial
--- Enter New Values ---
serial bit rate [9600]: 19200
serial data bit [8]: 
serial parity [none]: 
serial stop bit [1]: 
serial flow control [none]: 
use null modem (rolled cable to device)? (y/n) [n]: 
Do you want to commit these changes? (y/n): y
```

Issue the **terminal binary** command to start a terminal session with the ACU.  This session takes place within your Uplogix Local Manager session.

```
[admin@UplogixLM (port1/3)]# terminal binary
```

At this point, you should see Intellian command codes in your terminal session.>
â€ƒ
# Configuring the Arbitrator (Mediator)

The Intellian Arbitrator is designed to switch RF communications between two Intellian ACUs. The Arbitrator is configured exactly as the ACU and uses similar cabling.  

![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image003.jpg)

# Advanced Features

Through a feature called Terminal Mirror, Uplogix can provide ACU access to the Intellian V-Series PC Controller application using SSH or the Uplogix CLI applet. 

## V-Series PC Controller access

Terminal Mirror can be used with the Uplogix CLI Applet or a Secure Shell (SSH) client. The Terminal Mirror feature is designed to forward information via the Intellian ACU or Arbitrator through the Uplogix Local Manager to the technicianâ€™s PC on a local TCP port. The application then connects to the user workstation â€œlocalhostâ€ (127.0.0.1) and port to manage the unit.

From the Uplogix Control Center, log into the Local Manager using SSH or Uplogix CLI Applet and navigate to the port where the Intellian ACU is connected. The CLI button uses secure shell. The Dial button (visible if configured) will used the Remote Application Server (RAS) to dial into the appliance.

![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image004.png)

After logging into Uplogix Local Manager, navigate to the port with the antenna to manage and enter the command **terminal binary**.

After connecting, click on the Terminal command from the Terminal Applet window and then select the Forward option.

![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image005.png)

Check the box for terminal mirror, and either leave the random TCP port selected or manually assign an unused local TCP port. Click *Apply*.

![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image006.png)

After applying changes for the local TCP port on the terminal mirror, the indicator will turn green to indicate the available port has been reserved or red to indicate the port selected is not available. You will use the TCP port within the Intellian V-Series PC Controller application. 
	
![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image007.png)

Launch the Intellian V-Series PC Controller and use the port specified in the previous step.

![](http://uplogix.com/support/docs/img/configuration-guides/intellian-image008.jpg)

