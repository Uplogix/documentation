# Overview
This guide will walk you through the initial deployment of an Uplogix Local Manager. Please ensure the Local Manager has already been physically installed in the rack using the following instructions:

* [Uplogix LM80/LM83X Local Manager - Physical Installation](https://uplogix.com/docs/local-manager-user-guide/series-8/physical-installation)
* [Uplogix 500/5000 Local Manager - Physical Installation](https://uplogix.com/docs/local-manager-user-guide/series-5/physical-installation)

# Power On
Use the power button on the front panel of the Local Manager to power on the system.

![Uplogix LM80 Diagram](https://uplogix.com/support/docs/img/6.0/uplogix-lm80-local-manager-diagram.png)

# Connect Local Manager to LAN

To manage the Local Manager and attached devices in-band through the network, connect Gigabit Ethernet port 0 (GE-0) on the front panel to your network using a straight Ethernet cable. Both GE-0 and GE-1 auto-negotiate their speed and duplex settings by default. 

Alternatively, if your management network is fiber-based, connect to the SFP. If GE-0 or GE-1 are connected to the network, they will take precedence over the fiber connection. 

When connected, secondary management Ethernet port GE-1 acts as a standby redundant Ethernet management connection by default. GE-1 will become active if the GE-0 link drops. Therefore, it is important that GE-0 and GE-1 be connected to switch ports in the same network or VLAN.

# Configure via LCD Screen and Keypad 

The keypad located on the front panel of the Local Manager provides up, down, left, and right keys (labeled with arrows) as well as enter (i.e. the middle key) and back keys. The left and right arrows move the cursor left and right, respectively. The up and down arrows change numerical values.

![Uplogix LM83X LCD](https://uplogix.com/support/docs/img/6.0/lm83x-lcd.png)

When you use the keypad, no username/password is required.

For each setting, you can accept the default or existing setting by pressing the enter key.

**(1)** Press the enter key on the keypad to access the menu. The > character appears to the left of the currently selected option. Press enter or the right arrow button to access the configuration screens.
```
>Configure
Restart
```
**(2)** The Local Manager can use a DHCP server for network addressing. Brackets appear around the selected option. Use the left and right arrows to select your response and press enter to advance. If you are using DHCP, press the enter key and skip to Step 6. You can review the assigned IP address after configuration is complete by re-entering the configuration dialog.
```
Use DHCP?
[Yes] No 
```

**(3)** If you choose not to use DHCP, enter the IP address that the Local Manager should use. Use the left and right arrows to move between digits of the IP address, and the up and down arrows to change individual digits. The > prompt points to the digit to be changed.
```
IP Address:
>000.000.000.000
```

When entering an IP address, built-in validation keeps the octet below 255 at all times. You may need to change the second digit before you can change the first digit.

For example, to change the number 180 to 240, you must change the second digit from 8 to 4 before you can change the first digit from 1 to 2. The validation will not allow an address 280, so the first character will toggle between 1 and 0 until you change the second character to keep the octet at or below 255.

**(4)** Configure the Local Manager's subnet mask in the same manner:
```
Netmask:
>255.255.255.000
```

**(5)** Specify a default route for network connectivity.
```
Default Route:
>000.000.000.000
```

**(6)** Whether you use DHCP or a static IP address, the Local Manager next prompts you to select speed and duplex options for the management Ethernet connection.
```
Speed/Duplex
<auto>
```
Auto-negotiation is the default setting. If you choose not to use auto-negotiation, select speed and duplexing to match your network.

Use the right arrow key to view other speed/duplex options. They appear as 1000full, 100full, 10full, 100half and 10half.

This setting needs to match the speed and duplex setting on the switch port that is connected to your Local Manager. 

**(7)** If a Pulse server is to be used, enter the IP address here. 
```
Pulse Server IP:
127.000.000.001
```
**(8)**	Enter an IP address for the Uplogix Control Center only if this unit is to be managed by an Uplogix Control Center. Otherwise, do not enter an IP address at this prompt. Press enter to skip to the next configuration item.
```	
Server IP:
>127.000.000.001
```

If the Local Manager has already been associated with an Uplogix Control Center that uses a DNS name, this prompt is not displayed.

**(9)** The Local Manager is now configured. Select Yes to save your changes.
```
Confirm Changes?
Yes [No]
```

If you have configured the Local Manager with a management IP address, you can now manage it remotely via an SSH session. Refer to Remote access via the management IP connection section of this guide.

<div class='info'>For security, you may disable the keypad after you finish the initial setup.</div>

**Initial setup of the Local Manager is now complete.**

# Connect a workstation

If no LCD Screen and Keypad is present, a console connection can be used to configure the Local Manager. The required hardware will vary based on your workstation's capabilities.

* If your workstation has a DB-9 serial port, use the DB-9 to RJ-45 adaptor provided by Uplogix and a straight-through Ethernet cable to connect to the console port.
* If your workstation does not have a DB-9 serial port, you will need to use a USB to DB-9 serial adaptor together with a straight Ethernet cable and the DB-9 adaptor provided by Uplogix to connect to the console port.

The default settings for the console port are 9600, 8, N, 1.

# Logging in for the first time

To configure the Local Manager via the CLI, connect directly to the console port on the front of the device. This port is labeled CON. The configuration options available via the keypad are also available through the command line. 

> If you have already configured the Local Manager's network settings via the front panel, you may choose to access the Local Manager via SSH.

Open a connection to the Local Manager using a terminal client on your computer. Supported terminal clients include: 

* Windows HyperTerminal 
* ZTerm (Macintosh OS X) 
* Minicom (Unix/Linux) 

The default console connection settings are 9600 baud, 8 data bits, 1 stop bit, no parity. For best results, set your terminal emulator to use ANSI encoding.

<div class='warning'>The Local Manager does not use flow control. If you use HyperTerminal, you must disable flow control when configuring the session.</div>

After you connect to the Local Manager, you will be prompted for a username and password. The default username is *admin* and the default password is *password*. Usernames and passwords are case-sensitive. 

Upon login, users will be presented with the system dashboard, which provides an overview of the connected devices.

```
Uplogix LMS v6.2 38768 -- Powering Business Uptime
------------------------------------------------------------------------------
Port     Hostname            Status        Con Eth Uptime   Processor   Last 
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
 1/1 AUS-CORE2          OK                  *   *  301d 5h    00/00/00        
 1/2                                        *   -                             
 1/3                                            -                             
 1/4                                            -                             
 1/5                                                                          
 1/6                                                                          
 MDM embedded                                                                 
 SYS UplogixLM          OK                      *  1d 6h      13/13/12 18s    
------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
                  d=day, h=hour, m=minute, s=second

Ports 1/1-1/4 have dedicated Ethernet.

[admin@UplogixLM]# 
```

# Assign an IP address

The Local Manager is initially configured to use DHCP. You can use the **show system ip** command to display current management Ethernet network settings. To configure the Local Manager's network addressing, use the **config system ip** command. 

The Local Manager displays the current settings and presents a prompt asking whether you want to make changes. 
```
[admin@UplogixLM]# config system ip
--- Existing Values --- 
Use DHCP: Yes 
Management IP: 0.0.0.0
Host Name: UplogixLM
Subnet Mask: 255.255.255.0 
Broadcast Address: 0.0.0.255 
Default Route: 0.0.0.0 
Speed/duplex: auto: 1000full
MAC Address: 00:0F:2C:00:CC:C6 
Bonding Link: yes
Primary Ethernet Link: yes (bonded)
Auxiliary Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values --- 
Use DHCP: (y/n) [y]: n
Management IP: [0.0.0.0]: 198.51.100.4
Host Name: [UplogixLM]: 
Subnet Mask: [255.255.255.0]: 
Default Route: [0.0.0.0]: 198.51.100.254
speed/duplex: [auto:1000full]: 
Use DNS (y/n) [y]: 
Automatically configure DNS (y/n) [y]: n
DNS Server IP 1: 172.30.4.252
DNS Server IP 2:  
Domain Search: 
Warning: Remote connections may be lost if you commit changes. 
Do you want to commit these changes? (y/n): y
```
The changes take effect after you commit them. 

If you have configured the Local Manager with a management IP address, you can now manage it remotely via an SSH session. 

# Enable management by an Uplogix Control Center

Use the **config system management** command to instruct the Local Manager to synchronize with an Uplogix Control Center. Use the default values, but set *Hostname or IP:* field to contain the hostname or IP address of your Control Center.

> The option *Hostname or IP:* is displayed if DNS is configured. If DNS is not enabled, *IP:* will be displayed instead.

```
[admin@UplogixLM]# config system management
--- Existing Values ---
Use Management Server: false
Hostname or IP: 127.0.0.1
Port: 8443
Heartbeat interval (seconds): 30
Heartbeat band: all
Always use minimal heartbeat: false
Last successful heartbeat:  (not yet contacted)
Change these? (y/n) [n]: y
--- Enter New Values ---
Use Management Server (y/n) [n]: y
Automatically configure Management Server (y/n) [n]: 
Hostname or IP [127.0.0.1]: 203.0.113.3
Port [8443]: 
Heartbeat interval (seconds) [30]: 
Heartbeat during [all]: 
Do you want to commit these changes? (y/n): y
```

See also: System Configuration / [Control Center Management](http://uplogix.com/docs/local-manager-user-guide/system-configuration/control-center-management)

# Create a new user (standalone)

To secure your Local Manager, create a new user for everyday use and disable the default admin user account.

Local Managers managed by an Uplogix Control Center will automatically inherit the security policy defined for the deployment. As such, all user accounts must be managed on the Control Center itself.

If you try to modify users on a managed Local Manager, you will receive the following message.

```
[admin@UplogixLM]# config user ajones
Users may not be edited when the system is managed.
```
To create a new user, use the **config system user** command.

```
[admin@UplogixLM]# config user ajones
User ajones does not exist. Create (y/n): y
[config user ajones]#
```

Assign the user the *admin* role on *all* resources on the Local Manager. Type *exit* to save the user.

```
[config user ajones]# all admin
[config user ajones]# exit
```

Set a password for the newly created user with the **config password** command.

```
[admin@UplogixLM]# config password ajones
New Password: ****
Confirm Password: ****
Password changed.
```

Switch to the new user's account with the **enable** command.

```
[admin@UplogixLM]# enable ajones
password: ****

[ajones@UplogixLM]# 
```

Edit the *admin* user account and disable it.

```
[ajones@UplogixLM]# config user admin
[config user admin]# disabled
[config user admin]# exit
```
Verify the *admin* account has been disabled by trying to **enable** as that user.
```
[ajones@UplogixLM]# enable admin
password: ********
Invalid password.
```

<div class='info'>The message <i>Invalid password</i> is presented for all login failures, regardless of actual cause (e.g. disabled account).</div>

# Initial Setup Complete

The Local Manager is now online, connected to the network, and optionally, being managed by Control Center.

Continue configuring the Local Manager by visiting the various topics in our Documentation Library.