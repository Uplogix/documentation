# Overview

The Local Manager can be configured to provide Out-of-Band access when the primary network connection becomes unavailable. 

<div class='ucc' />Inventory > Local Manager Summary > Out-of-Band > Setup Wizard</div>

Types of access:

* Mobile-terminated: The Local Manager acts as an endpoint by answering an attached modem.
* Mobile-originated: The Local Manager establishes a PPP connection (and optionally a VPN connect) via an attached modem (v92, cellular, Iridium, etc.)

Out-of-band connections can be initiated manually or automatically with the [Pulse feature](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/using-the-pulse-feature) or through the rules engine.

The following sections detail how to configure PPP and optional VPN (IPSec and PPTP) settings when necessary.

> If you are using a cellular modem, see [Getting Started with Cellular Modems](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/getting-started-cellular-modems)

# Configuring a modem

The following out-of-band options are supported:

* v.92 modem
* cellular modem (2G/3G/LTE)
* satellite modem (Iridium, GlobalStar)
* secondary ethernet

To initialize a modem, log into the Local Manager and navigate to the modem resource.

```
[admin@UplogixLM]# modem
 embedded   
 
[admin@UplogixLM (modem)]#
```

If your Local Manager shipped with an embedded modem (V.92 or cellular modem), the Local Manager software will automatically detect and configure the modem on boot.  Otherwise, use the **config init** command to initialize the modem.

```
[admin@UplogixLM (modem)]# config init
This device has already been initialized.
Would you like to reinitialize it? (y/n): y
--- Enter New Values ---
description: 
make [embedded]: Iridium
Serial Bit Rate [38400]: 
Serial Data Bit [8]: 
Serial Parity [none]: 
Serial Stop Bit [1]: 
Serial Flow Control [none]: 
Do you want to commit these changes? (y/n):
```

Based on the *make* provided, the Local Manager will automatically suggest a baud rate.

# Configuring a virtual modem

The Local Manager can be configured to connect to an external modem over Ethernet - this is achieved by configuring a virtual modem. A virtual modem will override an embedded modem when configured. Use the **config system slot modem** command to configure a virtual modem. 


> **Note: This feature is not often used.** As of LMS version 5.4.3, only Telnet works for PPP on a virtual modem port.      


```
[admin@UplogixLM]# config sys slot modem
[config system slot modem]# port 3 203.0.113.6 6003 telnet
Port 3 added.

```

# Configuring for dial-in access

<div class='ucc' />Inventory > Local Manager Summary > Out-of-Band > Modem</div>

> Dial-in access is not available on cellular modems.

Dial-in access is disabled by default for security. To enable dial-in access, use the **config answer** command from the modem resource.

```
[admin@UplogixLM (modem)]# config answer
[config answer]# 
```
The **config answer** command opens an editor when run. To view available subcommands, use the **?** command.

```
[config answer]# ?
Allowable arguments are:
show
enable
disable
[no] init <modem init string>
[no] allow <phone number>
[no] deny <phone number>
rings <number>
[no] ringback
[no] pulse
[no] logrings
[no] encryption [required]
[no] number <system phone number>
[no] domain <SMS domain name>
[no] apn <Cellular APN value>
or 'exit' to quit config mode
```

Here's what each setting does:

| Setting | Description |
| - | - |
| show | Displays the current answer settings |
| enable | Enables the dial-in feature<BR><BR>NOTE: This setting is ignored if *enable dial-in on Pulse failure* is enabled. | 
| disable | Disables the dial-in feature |
| [no] init "" {modem init string} | Sets the modem initialization string. The double quotes are **required**. |
| [no] allow {phone number OR all} | Specify a phone number or a range of phone numbers allowed to call in to the modem. For example, in the USA, allow 512 will permit access from any number in the 512 area code. To specify the range of numbers assigned to your organization, use allow 5128577.<BR><BR>To allow all numbers, or if Caller ID is not available, use **allow all**. |
| [no] deny {phone number OR all} | Specify a phone number or range of phone numbers that will be refused. |
| rings <number> | Specifies the number of rings before the call is answered. Default value is 3.
| [no] ringback | When enabled, the Local Manager ignores an incoming call until it hangs up. If the user calls back within a specified amount of time, the Local Manager answers the call. |
| [no] pulse | Enables dial-in on Pulse failure. Overrides *enable* setting. |
| [no] logrings | Enables inbound call attempts
| [no] encryption [required] | Enables dial-in encryption |
| [no] number {system phone number} | Stores the phone number of the modem. Used with satellite/cellular modems for SMS-initiated PPP. |
| [no] domain {SMS domain name} | Stores the email-to-text domain of the modem. Used with satellite/cellular modems for SMS-initiated PPP. |
| [no] apn >Cellular APN value< | Sets the APN for a cellular modem |

If the Local Manager is managed by a Control Center, the modem can be configured through the Uplogix web interface.

# Enabling Caller ID on v92 Modems

To enable Caller ID on the embedded modem, the init string will need to be updated from the default ATZ.

Use the **config answer** command to edit the init string.

```
[admin@UplogixLM]# modem
[admin@UplogixLM (modem)]# config answer
[config answer]# init "" \\d\\d\\d+++\\d\\d\\dATH0 OK ATZ OK ATS7=45S0=0L1V1X4&C1E1Q0 OK AT+VCID=1
```

The init string shown above is for use with embedded modems only. Other modems (Iridium, Multitech, etc.) may require different init strings. Be sure to use the **allow** subcommand to specify which numbers are allowed to call the Local Manager.


# Configuring for dial-out access

<div class='ucc' />Inventory > Local Manager Summary > Out-of-Band > PPP</div>

To enable out-of-band communication with the Local Manager, use the **config ppp** command in the modem resource to configure PPP settings.

```
[admin@UplogixLM (modem)]# config ppp
--- Existing  Values ---
Phone Number: 
User Name:  
Password: ******** 
Use Static IP Address: false 
Use DNS: auto
Suspend SLV on Out-of-Band: yes
Enable Out-of-Band Sharing: no
Change these? (y/n) [n]:  y
--- Enter New Values ---
Phone Number: 1234567890
User Name: uplogix
Password: *******
Confirm Password: *******
Use Static IP Address (y/n) [n]: n
Use DNS (y/n/auto) [auto]: y
Suspend SLV on Out-of-Band (y/n) [y]: y
Enable Out-of-Band Sharing (y/n) [n]: n
Do you want to commit these changes? (y/n): y 
```

Here are the available settings:

| Setting | Description |
| - | - |
| Phone Number | The phone number of the remote access server that will terminate the PPP connection. |
| User Name | Used to authenticate the PPP connection with the dial-up service provider / remote access server. |
| Password | Used to authenticate the PPP connection with the dial-up service provider / remote access server. |
| Use Static IP Address | PPP connections use DHCP by default. Enter **y** to assign a static IP address to the PPP connection. |
| Use DNS | **Reserved for future functionality.** |
| Suspend SLV on Out-of-Band | Service Level Validation (SLV) tests will not run over the out-of-band network by default. Enter **y** to enable SLV tests to run over the out-of-band network connection. |
| Enable Out-of-Band Sharing | The WAN Traffic Failover (WTF) feature shares the out-of-band connection with a local router during a WAN failure. Enter **y** to turn the WTF feature on and allow the Local Manager to share its out-of-band connection with a local router. |

# Configuring VPN Settings

<div class='ucc' />Inventory > Local Manager Summary > Out-of-Band > VPN</div>

To configure the Local Manager to use a VPN server while operating out-of-band, use the interactive **config vpn** command in the modem resource to configure IPsec or PPTP settings.

## IPSec

To configure IPsec, the command presents this dialog:

```
[admin@UplogixLM]# modem
 embedded
[admin@UplogixLM (modem)]# config vpn
--- Existing  Values ---
VPN type: none
Change these? (y/n) [n]: y
--- Enter New Values ---
VPN type [none]: ipsec
Vendor [cisco]:
IPsec Server Hostname or IP: 203.0.113.1
IKE DH Group [dh2]:
Perfect Forward Secrecy [server]:
NAT Traversal Mode [none]:
Allow Single DES (y/n) [n]:
Deny MD5 (y/n) [n]:
Group ID:
Shared key:
User Name:
Password:
Do you want to commit these changes? (y/n):
```

## PPTP 

To configure PPTP, the command presents this dialog:

```
[admin@UplogixLM (modem)]# config vpn
--- Existing  Values ---
VPN type: none
Change these? (y/n) [n]: y
--- Enter New Values ---
VPN type [none]: pptp
PPTP Server Hostname or IP: 198.51.100.105
User Name:
Password:
Do you want to commit these changes? (y/n):
```

# Validating dial-out access

The PPP Cycle feature allows the Local Manager to bring up its out-of-band connection for a specified duration. When called from a scheduled job, this feature can regularly validate the Local Manager's out-of-band capability (modem+PPP/secondary Ethernet and VPN functionality). For devices in remote locations, the **ppp cycle** command can be used to test the end-to-end out-of-band connection by establishing the connection long enough to communicate briefly with the Control Center, and then tearing it down.

## Requirements

* Configured modem or secondary Ethernet configured for *outband*
* Configured PPP settings (n/a for secondary Ethernet)
* Configured VPN settings (if using VPN)

## ppp on / off

The **ppp on** and **ppp off** commands bring up and tear down the PPP connection. 

Manual activation of the PPP connection is often used prior to maintenance that may impact the in-band connection to the Local Manager.

## ppp cycle

The **ppp cycle** command brings up the out-of-band connection for a specified duration or long enough to execute a single heartbeat with the Control Center.

> This command is useful for troubleshooting. Even if PPP settings are incorrect or cause the Local Manager to become inaccessible, **ppp cycle** will tear down the connection and restore inband access after the specified duration or heartbeat attempt.

### ppp cycle duration

The **ppp cycle duration** command will complete the following actions:

* Turn PPP on
* Display the out-of-band IP address (will show PPP and VPN addresses)
* Wait one minute
* Turn PPP off

Use **ppp cycle duration** from the modem resource to execute a one-time PPP test. The device will remain out-of-band for one minute (default duration) before it disables PPP. Use the -d flag to change the duration in minutes.

```
[admin@UplogixLM (modem)]# ppp cycle duration
Secondary network Local Address is 192.0.2.225
Out of Band is turned on
Waiting 1 minutes
Waited 1 minutes; Out of Band is up
Done waiting
Out of Band is turned off
Out of Band Cycle: OK
```

### ppp cycle heartbeat

The **ppp cycle heartbeat** command will complete the following actions:

* Turn PPP on
* Display the out-of-band IP address
* Send one heartbeat to the Control Center
* Display Control Center heartbeat version for verification
* Turn PPP off

Run **ppp cycle heartbeat** from the modem resource to execute a one-time PPP test. Use the -m flag to specify minimal heartbeat mode (for low-bandwidth OOB connections). 

```
[admin@UplogixLM (modem)]# ppp cycle heartbeat
Secondary network Local Address is 192.0.2.100
Out of Band is turned on
Attempting heartbeat
Server heartbeat version: 4.7.24674
Heartbeat complete
Out of Band is turned off
Out of Band Cycle: OK	
```

# Modem Troubleshooting

Issue the **pull tech** command followed by the **show tech** command to display information about the modem that can be helpful when troubleshooting modem problems. Here is an example of the information collected from an internal GPRS cellular modem:

```
[admin@UplogixLM (modem)]# pull tech
Checking IMEI / Modem Serial Number
Checking Modem Firmware Version
Checking Modem Functionality Mode
Checking Network Registration State
Checking Signal Strength
Checking ICCID / SIM Card Number
Checking Network Operator Name
Checking International Mobile Subscriber Identity
Checking Mobile Directory Number
Checking PDP Context
Pull tech completed and saved as current. 

[admin@UplogixLM (modem)]# show tech
IMEI / Modem Serial Number (AT+CGSN):
    011998650336851

Modem Firmware Version (AT+CGMR):
    R7.45.1.201105250600.WMP50 2203572 052511 06:00

Modem Functionality Mode (AT+CFUN?):
    Mobile full functions with power saving disabled. (1)

Network Registration State (AT+CREG?):
    Registered, home network. (0,1)

Signal Strength (AT+CSQ):
    (-67) dBm.

ICCID / SIM Card Number (AT+CCID):
    "89014346712409549491"

Network Operator Name (AT+CPHS=2,5):
    AT&T

Mobile Country Code (AT+CIMI):
    310

Mobile Network Code (AT+CIMI):
    410

Mobile Subscriber Identification Number (AT+CIMI):
    240954949

Mobile Directory Number (AT+CNUM):
    15558675309

PDP Context (AT+CGDCONT?):
    1,"IP","ccspbdd322.acfes.org",,0,0
```
