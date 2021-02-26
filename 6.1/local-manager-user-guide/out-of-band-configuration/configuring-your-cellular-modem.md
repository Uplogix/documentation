# Overview
This article describes the configuration of a Local Manager with a cellular modem.

Before following the steps in this guide, ensure you have already completed [Getting Started with Cellular Modems](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/getting-started-cellular-modems).
# Resource Configuration

Log into the Local Manager and access the modem resource using the **modem** command. Embedded modems should automatically configure the appropriate carrier settings for most modems. Others must be configured with the **config init** command before the cellular modem can be used. When prompted for make, use *cellular*.â€¯

```
[admin@UplogixLM]# modem
embedded

[admin@UplogixLM (modem)]# config init
 This device has already been initialized.
Would you like to reinitialize it? (y/n): y
--- Enter New Values ---
description: []: <good place for assigned IP address or 10 digit phone number> 107.80.100.112â€¯ 
make: [embedded]: cellularâ€¯ 
serial bit rate [115200]:â€¯â€¯ 
serial data bit [8]:â€¯â€¯ 
serial parity [none]:â€¯â€¯ 
serial stop bit [1]:â€¯â€¯ 
serial flow control [none]:â€¯â€¯ 
Enable Out-of-Band Sharing: (y/n) [n]â€¯ 
Do you want to commit these changes? (y/n): yâ€¯ 
Testing login will take a few moments...â€¯ 
Login successful; credentials are valid.â€¯ 
```
   
# Configure Carrier (LTE CAT 4 Combo / MNA-1 Modems ONLY)
MCT-MNA1 and MTD-MNA1 modems use a cellular radio with dual firmware, meaning the device can connect to two different carrier networks (not simultaneously). The modem can operate on either Verzion or AT&T/other networks. Modems are factory defaulted for AT&T/other, but may be configured by Uplogix prior to shipment.

This section applies to the following parts only:

* 61-5009-40  -  Verizon CAT4 for 500/5000
* 61-5009-43  - AT&T CAT4   for 500/5000
* 88-CAT4VA - Verizon for LM80/LM83X
* 88-CAT4ATTA - AT&T for LM80/LM83X

## To check that your modem is configured for the desired network:

Open a terminal session with the modem, and run the following command:

```
AT#FWSWITCH?
```

If the response is **#FWSWITCH: 0**, the modem is configured for AT&T/other network.
If the response is **#FWSWITCH: 1**, the modem is configured for Verizon.

## To switch carrier networks:

**From AT&T to Verizon:**

```
AT#FWSWITCH=1,1
```

**From Verizon to AT&T:**

```
AT#FWSWITCH=0,1
```


# Testing Connectivity

Use the **pull tech** command and subsequently the **show tech** to view current modem state.â€¯â€¯

```
[admin@UplogixLM (modem)]# pull techâ€¯ 
Checking Modem Modelâ€¯ 
Checking IMEI / Modem Serial Numberâ€¯ 
Checking Modem Firmware Versionâ€¯ 
Checking Modem Functionality Modeâ€¯ 
Checking Network Registration Statusâ€¯ 
Checking Packet Service Typeâ€¯ 
Checking SIM Statusâ€¯ 
Checking ICCID / SIM Card Numberâ€¯ 
Checking Serving Cell Informationâ€¯ 
Checking International Mobile Subscriber Identityâ€¯ 
Checking Mobile Directory Numberâ€¯ 
Checking PDP Contextâ€¯ 
Checking 3G Statusâ€¯ 
Pull tech completed and saved as current.â€¯

[admin@UplogixLM (modem)]# show tech

Modem Model (ATI4):LE910-NAGâ€¯ 
IMEI / Modem Serial Number (AT+CGSN): 358942053034985â€¯ 
Modem Firmware Version (AT+CGMR):â€¯ 17.00.503â€¯ 
Modem Functionality Mode (AT+CFUN?): Mobile full functions with power saving disabled. (1)â€¯ 
Network Registration Status (AT+CGREG?): Registered, home network. (0,1)â€¯ 
Packet Service Type (AT#PSNT?): Unsolicited result code disabled. (0)â€¯ LTE network. (4)â€¯ 
SIM Status (AT#QSS?): SIM INSERTED. (0,1)â€¯ 
ICCID / SIM Card Number (AT#CCID): 89014103761238227â€¯ 
Network Operator Name (AT#SERVINFO): AT&Tâ€¯ 
Signal Strength (AT#SERVINFO):â€¯ (-86) dBm.â€¯ 
Mobile Country Code (AT+CIMI):â€¯â€¯â€¯ 310â€¯ 
Mobile Network Code (AT+CIMI):â€¯â€¯â€¯ 410â€¯ 
Mobile Subscriber Identification Number (AT+CIMI): 906743222â€¯ 
Mobile Directory Number (AT+CNUM):15125551211â€¯ 
PDP Context (AT+CGDCONT?):â€¯ 
â€¯â€¯â€¯ 1,"IP","broadband","",0,0â€¯ 
â€¯â€¯â€¯ 2,"IPV4V6","ims","",0,0â€¯ 
â€¯â€¯â€¯ 3,"IPV4V6","sos","",0,0â€¯ 
3G Status (AT#RFSTS):â€¯ 
â€¯â€¯â€¯ "310 410",2225,-116,-86,-8,700D,1,,128,19,0,00001D7,"310410906958822","AT&T",3,4â€¯ 
â€¯â€¯â€¯ Network-LTE (16)â€¯ 
â€¯â€¯â€¯ Country code and operator code: "310 410" (MCC, MNC)â€¯ 
â€¯â€¯â€¯ E-UTRA Assigned Radio Channel: DL=2,137.5 MHz, UL=1,737.5 MHz (2225)â€¯ 
â€¯â€¯â€¯ Reference Signal Received Power: -116â€¯ 
â€¯â€¯â€¯ Received Signal Strength Indication: -86â€¯ 
â€¯â€¯â€¯ Reference Signal Received Quality: -8â€¯ 
â€¯â€¯â€¯ Tracking Area Code: 700Dâ€¯ 
â€¯â€¯â€¯ Routing Area Code: 1â€¯ 
â€¯â€¯â€¯ Tx Power: -â€¯ 
â€¯â€¯â€¯ Discontinuous reception cycle Length: 128 msâ€¯ 
â€¯â€¯â€¯ Mobility Management: IDLE (19)â€¯ 
â€¯â€¯â€¯ Radio Resource Control: INACTIVE (0)â€¯ 
â€¯â€¯â€¯ Cell ID: 00001D7â€¯ 
â€¯â€¯â€¯ International Mobile Station ID: "3104109068765432"â€¯ 
â€¯â€¯â€¯ Operation Name: "AT&T"â€¯ 
â€¯â€¯â€¯ Service Domain: CS+PS (3)â€¯ 
â€¯â€¯â€¯ Active Band: AWS-1 (4)

```



Use the **terminal** command to ensure a good connection with the modem. After establishing a console session, AT commands like **ATZ** or **AT+CSQ** should return 'OK'.


```
[admin@UplogixLM (modem)]# terminal
Press ~[ENTER] to exit
Connecting ...
Console session started.
atz
OK
at+csq
+CSQ: 21,0
OK
```
To determine if the modem is properly connecting to the cellular network, use the **AT+CGREG?** command. The network registration status is also listed in the **show tech** output. The command will return one of the following responses:

- 0,0 â€“ The modem is not registered on any network
- 0,1 â€“ The modem is registered on the home network
- 0,2 â€“ The modem is not connected to the network
- 0,3 â€“ The modem is not connected to the network
- 0,5 â€“ The modem is registered on a network and it is roaming

For proper operation, **AT+CGREG?** should respond with 0,1.

#Configure Answer Settings

The **config answer** command allows you to specify device-specific information such as initialization string, phone number, and SIM card domain. If you will be using [SMS-initiated PPP](https://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/sms-initiated-ppp), the number and domain are required.â€¯ â€¯ 
```
[admin@UplogixLocalManager (modem)]# config answer
[config answer]# number 5125551212
[config answer]# domain text.provider.netâ€¯ 
[config answer]# exitâ€¯ 
```
Note that **text.provider.net** will need to be substituted for the SMS domain used by your provider.

Verify your settings with the **show answer** command.â€¯ 

```
[admin@UplogixLocalManager (modem)]# show answerâ€¯ 
disabledâ€¯ 
SLV suspended when PPP onâ€¯ 
answer after 3 ringsâ€¯ 
number 5125551212â€¯ 
domain text.provider.netâ€¯ 
```

# Configure APN

Unless your carrier provisions the modem Over the Air (OTA), the APN on the SIM will need to be set with your providerâ€™s custom APN designation. Think of it as a speed dial where the APN is the number and the PPP process dials entry 1. You should get this information from your cell provider account representative. The APN can also be entered in the Control Center in either the modem settings for the hierarchy group or in the individual Local Manager's modem settings page.


## Version 6.0

To configure the APN on a modem, use the **show apn** command.

```
[admin@UplogixLM (modem)]# config apn
Cellular APN: provider.apn.com
```

Common APN values:
* AT&T: BROADBAND, i2gold
* T-Mobile: fast.t-mobile.com
* Verizon: vzwinternet

## Version 5.5 and lower

To configure the APN(s) on a modem, open a **terminal** session and use the **AT+CGDCONT** command.

For **Verizon** modems (enter all 3):

```
AT+CGDCONT=1,"IPV4V6","vzwims"
AT+CGDCONT=2,"IPV4V6","vzwadmin"
AT+CGDCONT=3,"IPV4V6","provider.apn.com"
```

For **AT&T** modems:

```
AT+CGDCONT=1,"IP","provider.apn.com"
```

For both types of modems, note that **provider.apn.com** will need to be replaced with your providerâ€™s custom APN designation.

Exit the terminal session then check that the APN has been set using the **show apn** command.

```
[admin@UplogixLM (modem)]# show apnâ€¯ 
Cellular APN: provider.apn.comâ€¯
```

## Configure Initialization String (if required)

The initialization string can be used to designate the APN of your service provider for use with PPP. However, this method is no longer necessary/recommended as of LMS version 5.4. See the previous **Configure APN** section if you are running 5.4 or later.

Use the **config answer** command to add an initialization string.

For 5.4 and later:

```
[admin@U500 (modem)]# config answer
[config answer]# init "" ATZ
[config answer]# exit

```

For 5.3 and prior:

```
[admin@U500 (modem)]# config answer
[config answer]# init "" ATZ OK AT+CGDCONT=1,\"IP\",\"provider.apn.com\"
[config answer]# exit
```

**Note:** The quotes used in the AT+CGDCONT command require the â€œ\â€ escape character.

**Note:** CDMA modems do not require the APN designation command â€œAT+CGDCONTâ€ for proper operation. If you are using a CDMA modem, please use this alternate init string:

```
[config answer]# init "" ATZ
[config answer]# exit
```

Verify your settings with the **show answer** command.

```
[admin@U500 (modem)]# show answer
disabled
SLV suspended when PPP on
init "" ATZ OK AT+CGDCONT=1,\"IP\",\"provider.apn.com\"
answer after 3 rings
number 5125551212
domain text.provider.net
```

Please note that **provider.apn.com** will need to be replaced with your providerâ€™s custom APN designation. You will be able to get this information from your cell provider account representative. In addition **text.provider.net** will need to be substituted for the text message domain used by your provider
    
### Initialization Strings Explained

The initialization strings for cellular modems are more complex than typical V.92 modems. Below is a brief explanation of each element of the cellular-specific init string.

<table>
<tr><td><strong>ATZ</strong></td>
<td>Restores the default configuration of the modem.</td></tr>
<tr><td><strong>AT+CGDCONT=1</strong></td><td>
Defines the use of PDP (packet Data Protocol) context, will be followed by connectivity type and APN.</td></tr>
<tr><td><strong>â€œIPâ€</strong></td>
<td>Sets the modem to use IP connectivity.</td></tr>
<tr><td><strong>â€œprovider.apn.comâ€</strong></td>
<td>The APN designation set up by your provider</td></tr>
</table>

# Set Modem Frequency (if required)

The modemâ€™s default quad-band mode may not work outside of North America. You may need to set the frequency to the appropriate mono-band to use the modem in other locations.

To check the current band: **AT+WMBS?**

To restore the modem to the default North America settings, use: **AT+WMBS=7,1**

The syntax of the command is **AT+WMBS=(band),(param)**

**Supported Bands:**

<table><tr><td><strong>0</strong></td><td>mono-band 850 MHz</td></tr><tr><td><strong>1</strong></td><td>mono-band 900 extended MHz (900E)</td></tr><tr><td><strong>2</strong></td><td>mono-band 1800 MHz</td></tr><tr><td><strong>3</strong></td><td>mono-band 1900 MHz</td></tr><tr><td><strong>4</strong></td><td>dual-band 850/1900 MHz</td></tr><tr><td><strong>5</strong></td><td>dual-band 900E / 1800 MHz</td></tr><tr><td><strong>6</strong></td><td>dual-band 900E / 1900 MHz</td></tr><tr><td><strong>7</strong></td><td>quad-band 850/900E/1800/1900 MHz</td></tr></table>

**Parameters:**

<table><tr><td><strong>0</strong></td><td><strong>Default</strong>. The wireless modem must be reset to start using the specified band. </td></tr><tr><td><strong>1</strong></td><td>The change is effective immediately. The GSM stack is restarted on the specified band.</td></tr></table>

#  Configure PPP (Outband) Settings

Most Outband settings should be automatically configured on Local Manager startup. If not, they can be manually entered.

Out-of-band sharing, or tethering, can be enabled to forward traffic from most Local Manager Ethernet ports when Outband mode is active.â€¯Each port must be individually configured to forward traffic, and is ONLY configurable after this setting is enabled. 
```
[admin@UplogixLocalManager (modem)]# config pppâ€¯ 
--- Existingâ€¯ Values ---â€¯ 
Phone Number: *99***1#â€¯ 
User Name:â€¯â€¯â€¯ 
Password: ********â€¯â€¯ 
Use Static IP Address: falseâ€¯â€¯ 
Change these? (y/n) [n]: yâ€¯ 
--- Enter New Values ---â€¯ 
Phone Number:[]: *99***1#â€¯ 
User Name: []: usernameâ€¯ 
Password []: ********â€¯ 
Confirm Password: ********â€¯ 
Use Static IP Address: (y/n) [n]:â€¯â€¯ 
Enable Out-of-Band Sharing: (y/n) [n]â€¯ 
Do you want to commit these changes? (y/n): yâ€¯ 
```
**Note:** For CDMA and EV-DO modems, use **#777** as the phone number. Consult your service provider for more information.

# Configure SMS monitor for SMS-initiated PPP (outband)

The Uplogix Local Manager can be configured to monitor incoming SMS text messages (sent by the Control Center) to determine if it should establish an Outband connection. This can be accomplished with a modem monitor and a default rule named **smsPppOn**.â€¯ 

```
[admin@UplogixLM (modem)]#â€¯config monitor sms smsPppOnâ€¯ 
Job was scheduled 0: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor sms none smsPppOn 30â€¯ 
```

###Testing SMS/Outband from Control Centerâ€¯ 

To initiate an outband connection from the Control Center, navigate to the local manager detail page and click on **Schedule Task**. From the drop-down task menu, select SMS Message and click Next. As of LMS 5.5, the only available option is **PPP On**. Click Next to send the SMS message.â€¯ 

###Error Messagesâ€¯ 

**Failed to send SMS message** â€“ SMS messages are sent using an e-mail to SMS gateway. To send messages, the Control Center must be properly configured to send e-mail. Check the SMTP settings under *Administration -> Server Settings -> Mail Settings*.

**Note:** SMS-initiated PPP is not currently supported for Verizon CDMA modems.

#Testing Outband from Local Manager

To initiate an Outband connection from the Local Manager, navigate to the system or modem context and execute **outband cycle duration**. This will cycle the Outband connection for the default of 1 minute andâ€¯return inband at the end of the minute.â€¯â€¯â€¯ 
```
[admin@UplogixLocalManager (modem)]# outband cycle durationâ€¯ 
Turning on Secondary Networkâ€¯ 
PPP ...â€¯ 
> CONNECTâ€¯ 
PPP Local Address: 107.80.100.112â€¯ 
Out-of-Band is turned on.â€¯ 
Waiting 1 minutesâ€¯ 
Waited 1 minutes; Out-of-Band is upâ€¯ 
Done waitingâ€¯ 
Turning off PPPâ€¯ 
Out-of-Band is turned offâ€¯ 
Out-of-Band Cycle: OKâ€¯ 
```
Using the similar option of **heartbeat** will additionally validate that Heartbeat successfully communicated over the outband connection.â€¯ 

```
[admin@UplogixLocalManager (modem)]# outband cycle heartbeatâ€¯ 
Out-of-Band Cycle: OKâ€¯ 
```
**Note:** If the Outband connection is not routable to the client workstation over ssh, the connection may hang or drop.â€¯ 

**Note:** If the appliance fails to establish an Outband connection, try populating the username and password fields in **config ppp** with arbitrary values. Some providers require a username and password to be sent, even if no authentication is taking place.â€¯ 

#Testing Outband from Control Center

To initiate an Outband connection from the Control Center, navigate to the Local Manager detail page and click on **Schedule Task**. From the drop-down task menu, select **PPP** and click Next. Select the mode from the following screen:

![PPP On UCC](http://uplogix.com/support/docs/img/PPP-on-UCC.jpg)


Click Next to select the scheduled time/date. The default is the current time.â€¯ 


To validate, run **show events** events from the CLI or click "Events" on the UCC Web interface.
```
[admin@UplogixLM]# show eventsâ€¯ 
UCTâ€¯â€¯â€¯â€¯â€¯â€¯ Contextâ€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯ Messageâ€¯ 
-----â€¯â€¯â€¯â€¯ ------------------â€¯â€¯â€¯â€¯ ---------------------------------------â€¯ 
11:58â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯ PPP is up. (107.80.100.112)â€¯â€¯ 
11:58â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯ PPP is down.â€¯ 
11:58â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯â€¯ PPP cycle heartbeat completed.
```

# Troubleshooting

The following terminal commands may be useful in the troubleshooting of cellular modems. For more information about these commands, please consult the Multitech Support Portal.

**AT+CCID**

Returns the modemâ€™s CCID number.

**AT+CFUN**

Selects the mobile stationâ€™s level of functionality.

	AT+CFUN?	Query current functionality level
	AT+CFUN=0	Set minimum functionality; run IMSI DETACH procedure
	AT+CFUN=1	Set full functionality; restart GSM stack

**AT+CGSN**

Returns the modemâ€™s IMEI number.

**AT+CMGL**

Queries the modem for SMS messages.

	AT+CMGL=0	Show unread messages
	AT+CMGL=4	Show all messages
	AT+CMGD=n	Delete message n

**AT+CNUM**

Returns the modemâ€™s phone number. Should match what is configured in config answer.

**AT+COPS**

Selects a Public Land Mobile Network (PLMN) acquisition method. 

	AT+COPS?	Queries for current PLMN
	AT+COPS=?	Queries for PLMN list
	AT+COPS=0	Set automatic mode (default)
	AT+COPS=1	Set manual mode
	AT+COPS=2	Deregister
	AT+COPS=4	Set manual mode with fallback to automatic mode

**AT+CPOF**

Stops the GSM software stack as well as the hardware layer or modem activity.

	AT+CPOF	Stop the GSM stack
	AT+CPOF=1	Stop the modem

**ATD**

Dials a phone number. Useful for testing dial-out capabilities.

**ATE1**

Turns on local echo.

**AT+IPR**

Sets the baud rate.

	AT+IPR=<baud rate>	Set modem baud rate.

**AT#RESET**

Resets the modem.

	AT#RESET=0	Reset the GSM stack and internal modem
	AT#RESET=1	Reset the internal modem only

# Configure Signal Strength Monitor (optional)

The Uplogix Local Manager can be configured to monitor the modem's signal strength and display it to the dashboard, as well as send alarms when functionality it denigrated.

To implement, copy and paste the below ruleset in its entirety into the system resource on the CLI and hit enter:

    conf rule no CellularSignalQuality0
    conf rule CellularSignalQuality0
    description Cellular Signal QualityAt0
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 0
    conditions
    modem.response matches "CSQ:\s0,"
    exit
    exit
    
    conf rule no CellularSignalQuality1
    conf rule CellularSignalQuality1
    description Cellular Signal QualityAt1
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 1
    conditions
    modem.response matches "CSQ\s1,"
    exit
    exit
    
    conf rule no CellularSignalQuality2
    conf rule CellularSignalQuality2
    description Cellular Signal QualityAt2
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 2
    conditions
    modem.response matches "CSQ:\s2,"
    exit
    exit
    
    conf rule no CellularSignalQuality3
    conf rule CellularSignalQuality3
    description Cellular Signal QualityAt3
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 3
    conditions
    modem.response matches "CSQ:\s3,"
    exit
    exit
    
    conf rule no CellularSignalQuality4
    conf rule CellularSignalQuality4
    description Cellular Signal QualityAt4
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 4
    conditions
    modem.response matches "CSQ:\s4,"
    exit
    exit
    
    conf rule no CellularSignalQuality5
    conf rule CellularSignalQuality5
    description Cellular Signal QualityAt5
    action alarm -a "Cellular Signal Quality below minimum"
    action writeStatus Cell % is 5
    conditions
    modem.response matches "CSQ:\s5,"
    exit
    exit
    
    conf rule no CellularSignalQuality6
    conf rule CellularSignalQuality6
    description Cellular Signal QualityAt6
    action writeStatus Cell % is 6
    conditions
    modem.response matches "CSQ:\s6,"
    exit
    exit
    
    
    conf rule no CellularSignalQuality7
    conf rule CellularSignalQuality7
    description Cellular Signal QualityAt7
    action writeStatus Cell % is 7
    conditions
    modem.response matches "CSQ:\s7,"
    exit
    exit
    
    conf rule no CellularSignalQuality8
    conf rule CellularSignalQuality8
    description Cellular Signal QualityAt8
    action writeStatus Cell % is 8
    conditions
    modem.response matches "CSQ:\s8,"
    exit
    exit
    
    conf rule no CellularSignalQuality9
    conf rule CellularSignalQuality9
    description Cellular Signal QualityAt9
    action writeStatus Cell % is 9
    conditions
    modem.response matches "CSQ:\s9,"
    exit
    exit
    
    conf rule no CellularSignalQuality10
    conf rule CellularSignalQuality10
    description Cellular Signal QualityAt10
    action writeStatus Cell % is 10
    conditions
    modem.response matches "CSQ:\s10,"
    exit
    exit
    
    conf rule no CellularSignalQuality11
    conf rule CellularSignalQuality11
    description Cellular Signal QualityAt11
    action writeStatus Cell % is 11
    conditions
    modem.response matches "CSQ:\s11,"
    exit
    exit
    
    conf rule no CellularSignalQuality12
    conf rule CellularSignalQuality12
    description Cellular Signal QualityAt12
    action writeStatus Cell % is 12
    conditions
    modem.response matches "CSQ:\s12,"
    exit
    exit
    
    conf rule no CellularSignalQuality13
    conf rule CellularSignalQuality13
    description Cellular Signal QualityAt13
    action writeStatus Cell % is 13
    conditions
    modem.response matches "CSQ:\s13,"
    exit
    exit
    
    conf rule no CellularSignalQuality14
    conf rule CellularSignalQuality14
    description Cellular Signal QualityAt14
    action writeStatus Cell % is 14
    conditions
    modem.response matches "CSQ:\s14,"
    exit
    exit
    
    conf rule no CellularSignalQuality15
    conf rule CellularSignalQuality15
    description Cellular Signal QualityAt15
    action writeStatus Cell % is 15
    conditions
    modem.response matches "CSQ:\s15,"
    exit
    exit
    
    conf rule no CellularSignalQuality16
    conf rule CellularSignalQuality16
    description Cellular Signal QualityAt16
    action writeStatus Cell % is 16
    conditions
    modem.response matches "CSQ:\s16,"
    exit
    exit
    
    conf rule no CellularSignalQuality17
    conf rule CellularSignalQuality17
    description Cellular Signal QualityAt17
    action writeStatus Cell % is 17
    conditions
    modem.response matches "CSQ:\s17,"
    exit
    exit
    
    conf rule no CellularSignalQuality18
    conf rule CellularSignalQuality18
    description Cellular Signal QualityAt18
    action writeStatus Cell % is 18
    conditions
    modem.response matches "CSQ:\s18,"
    exit
    exit
    
    conf rule no CellularSignalQuality19
    conf rule CellularSignalQuality19
    description Cellular Signal QualityAt19
    action writeStatus Cell % is 19
    conditions
    modem.response matches "CSQ:\s19,"
    exit
    exit
    
    conf rule no CellularSignalQuality20
    conf rule CellularSignalQuality20
    description Cellular Signal QualityAt20
    action writeStatus Cell % is 20
    conditions
    modem.response matches "CSQ:\s20,"
    exit
    exit
    
    conf rule no CellularSignalQuality21
    conf rule CellularSignalQuality21
    description Cellular Signal QualityAt21
    action writeStatus Cell % is 21
    conditions
    modem.response matches "CSQ:\s21,"
    exit
    exit
    
    conf rule no CellularSignalQuality22
    conf rule CellularSignalQuality22
    description Cellular Signal QualityAt22
    action writeStatus Cell % is 22
    conditions
    modem.response matches "CSQ:\s22,"
    exit
    exit
    
    conf rule no CellularSignalQuality23
    conf rule CellularSignalQuality23
    description Cellular Signal QualityAt23
    action writeStatus Cell % is 23
    conditions
    modem.response matches "CSQ:\s23,"
    exit
    exit
    
    conf rule no CellularSignalQuality24
    conf rule CellularSignalQuality24
    description Cellular Signal QualityAt24
    action writeStatus Cell % is 24
    conditions
    modem.response matches "CSQ:\s24,"
    exit
    exit
    
    conf rule no CellularSignalQuality25
    conf rule CellularSignalQuality25
    description Cellular Signal QualityAt25
    action writeStatus Cell % is 25
    conditions
    modem.response matches "CSQ:\s25,"
    exit
    exit
    
    conf rule no CellularSignalQualityAbove25
    conf rule CellularSignalQualityAbove25
    description Cellular Signal QualityAt25
    action alarm -a "Cellular modem RSSI Above 25"
    action writeStatus Cell % is > 25
    conditions
    modem.response matches "CSQ:\s(?:(?:[2][5-9])|(?:[3-9][0-9])),"
    exit
    exit
    
    conf rule no CellularErrorMessage
    conf rule CellularErrorMessage
    description Cellular Error Message
    action powerCycle
    action alarm -a "Cellular modem returning errors"
    conditions
    modem.response matches "ERROR":2i AND
    NOT has-run powerCycle :5m
    exit
    exit
    
    config rule CellularNonResponsive
    action alarm -a "the modem has become unusable for 5 minutes, powercycling"
    action event GENERIC -a "the modem has become unusable for 5 minutes,  powercycling"
    action powerCycle
    action writeStatus no response powercycling
    conditions
    modem.response equals FAILED_TO_GET_RESPONSE :10i AND
    NOT has-run powerCycle :5m
    exit
    exit
    
    conf ruleset no CellularNative
    conf ruleset CellularNative
    description Cellular Rules for Multitech GPRS Cell Modems
    rules
    CellularNonResponsive, CellularErrorMessage, CellularSignalQuality25, CellularSignalQuality24, CellularSignalQuality23, CellularSignalQuality22, CellularSignalQuality21, CellularSignalQuality20, CellularSignalQuality19, CellularSignalQuality18, CellularSignalQuality17, CellularSignalQuality16, CellularSignalQuality15, CellularSignalQuality14, CellularSignalQuality13, CellularSignalQuality12, CellularSignalQuality11, CellularSignalQuality10, CellularSignalQuality9, CellularSignalQuality8, CellularSignalQuality7, CellularSignalQuality6, CellularSignalQuality5, CellularSignalQuality4, CellularSignalQuality3, CellularSignalQuality2, CellularSignalQuality1, CellularSignalQuality0, CellularSignalQualityAbove25
    exit
    exit

## Enable CellularNative ruleset

To use the CellularNative ruleset to monitor signal strength after the rules have been configured, run **config monitor modem CellularNative** from the modem resource. The default frequency is 30 minutes. 

```
[[admin@UplogixLM (modem)]# config monitor modem CellularNativeâ€¯ 
Job was scheduled 0: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor modemâ€¯30â€¯
```
