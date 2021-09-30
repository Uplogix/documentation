# Configure the Local Manager to recognize the modem

1.	Use a workstation to open a terminal or SSH session with the appliance.
2.	Use the **modem** command to navigate to the modem resource.
4.	Use the **config init** command to configure the Iridium modem. A baud rate of 19200 should be used.
```
[admin@UplogixLM (modem)]# config init
This device has already been initialized.
Would you like to reinitialize it? (y/n): y
--- Enter New Values ---
description: []: Iridium
make: [embedded]: Iridium
serial bit rate [38400]: 19200
serial data bit [8]: 
serial parity [none]: 
serial stop bit [1]: 
serial flow control [none]: 
Do you want to commit these changes? (y/n): y
Testing login will take a few moments...
Login successful; credentials are valid.
```
5. Issue the **terminal** command to start a terminal session with the modem. This takes place within your SSH or terminal session with the Local Manager. To exit at any time, use the ~[Enter] escape sequence.
```
[admin@UplogixLM (modem)]# terminal
Press ~[ENTER] to exit
Connecting ...
Console session started.
```
6. Issue **ati4** to verify communication with the modem.
```
ati4
IRIDIUM
OK
```
7.	If you are unable to issue commands to the Iridium modem, please see the troubleshooting steps in the following section.

# Troubleshooting the serial connection

Problems:

* "modem in use" messages
* "process is executing" messages
* No communication with the modem

Causes:

* Modem is disconnected
* Modem is powered off
* The cables connecting the Local Manager to the modem are incorrectly wired
* An incorrect init string is being us

Use the **show serial** command to modify the current serial settings and the **config answer** command to modify the initialization string.

# Unlock the modem's SIM card

Before the modem can access the Iridium network, it must be configured to use the installed SIM card. 

If the Iridium modem has already been configured and you have successfully placed or received calls, you may skip this section.

1.	Use the **terminal** command to access the modem's CLI.
2.	To view the status of the SIM card, use the** AT+CLCK=?** command. Depending on the firmware revision of your modem, the response will be +CLCK: followed by a string of two-character values. If the SIM card is unlocked, an "SC" value will be displayed.
3.	If the SIM card is locked (no "SC" listed), issue the following commands:
```
AT+CPIN="1111"
AT+CLCK="SC",0,"1111"
```
4.	Run the **AT+CLCK=?** command again to verify that "SC" is listed.
5.	If the SIM card will not unlock, ensure that it is properly seated and in the correct orientation.

## Verify signal quality

Signal quality is vital to the reliable performance of the appliance and modem.

1.	Use the **terminal** command to access the modem's CLI.
2.	Check signal quality with the **AT+CSQ?** command.
```
AT+CSQ?
+CSQ:4
OK
```
3.	If the signal is below 4, check antenna placement.
Automatic signal quality monitoring is discussed in a later section.

# Disable the modem's auto-answer function

The Local Manager answers incoming calls by watching for RING statements and then issuing the ATA command. If the modem is configured to answer automatically, it will interrupt this process.

1.	Use the **terminal** command to access the modem's CLI.
2.	Issue the following commands to disable auto-answer and save the configuration.
```
ATS0=0
AT&W
```

# Verify dial-in and dial-out functionality

Before testing the automated features of the Uplogix appliance, ensure that the Iridium can place and receive calls.

1.	Use the terminal command to access the modem's CLI.
2.	Test dial-in by calling the Iridium modem with another Iridium, a RUDICS gateway, or a regular telephone. The modem should display a RING statement when the data number is dialed.
	1.	Call from Iridium: Use the "atd00 + phone number" command.
	2.	Call from RUDICS: Use the "atdi00 + phone number" command.
	3.	Call from phone: Dial 011 + data phone number.
3.	Test dial-out by calling another Iridium or a regular telephone.
	1.	Call to Iridium: Use the "atd00 + phone number" command.
	2.	Call to phone: Use the "atd+1 + area code and phone number" command.

# Configuring for dial-in access

To enable dial-in access, use the **config answer** command in the modem resource. Then enter the following subcommands:

* **enabled** - Turns on the appliance's answering feature (**required**) 
* **init "" \d\d\d+++\d\d\dATH&F OK AT&K0+CBST=71,0,1**
	* This Iridium initialization string is **required** for proper operation.
* **allow all** - Since Iridium does not support Caller ID, the appliance must be instructed to accept all incoming calls (**required**)
* **rings 1** - Instructs the Local Manager to answer incoming calls after 1 ring.
* **number** - Stores the phone number of the Iridium modem.
	* If using SMS to activate PPP, this should be the phone number of the voice line.
* **domain** - For use with SMS-initiated PPP, this should be set to msg.iridium.com. Not required for any other features.

For example:

```
[admin@UplogixLM (modem)]# config answer
[config answer]# enable
[config answer]# init "" \d\d\d+++\d\d\dATH&F OK AT&K0+CBST=71,0,1
[config answer]# allow all
[config answer]# rings 1
[config answer]# number 881655551111
[config answer]# domain msg.iridium.com
[config answer]# exit
```

# Configuring for dial-out access (Generic PPP)

To configure PPP settings, use the **config ppp** command in the modem resource. You will need your service provider's phone number and username/password if required.

```
[admin@UplogixLM (modem)]# config ppp
--- Existing  Values ---
Phone Number: 
User Name:  
Password: ******** 
Use Static IP Address: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Phone Number:[]: +15125550101
User Name: []: username
Password [****]: ********
Confirm Password: ********
Use Static IP Address: (y/n) [y]: n
Do you want to commit these changes? (y/n): y
```

To test the PPP settings, use the **ppp cycle** command.

# Configuring for dial-out access (RUDICS VPN PPP)

Similar to the standard PPP configuration, a RUDICS VPN scenario additionally requires a static IP address. The dial-up phone number and static IP address will be provided by Iridium.

```
[admin@UplogixLM (modem)]# config ppp
--- Existing  Values ---
Phone Number: 
User Name:  
Password: ******** 
Use Static IP Address: false 
Change these? (y/n) [n]: y
--- Enter New Values ---
Phone Number:[]: 0088160000555
User Name: []: arbitrary_username
Password []: ********
Confirm Password: ********
Use Static IP Address: (y/n) [n]: y
Static IP Address: []: 192.168.100.1
Do you want to commit these changes? (y/n): y
```

> **NOTE:** While the PPP server does not support authentication, arbitrary text is required in the User Name field on the appliance. PPP connections will fail if this field is left empty.

To test the PPP settings, use the **ppp on** and **ppp off** command.

# Configuring for SMS-initiated PPP

This feature allows you to activate PPP from the Control Center when an LM has stopped heartbeating. The Control Center will send an encoded message to an Iridium gateway that converts it to SMS and delivers it to the Iridium modem.

To activate PPP when an SMS message is received, the LM must be configured to check for messages. This can be accomplished with the **config monitor sms** command and **smsPppOn** rule.

```
[admin@UplogixLM (modem)]# config monitor sms smsPppOn :60
Validate scheduled monitor(sms)?  (This will execute the job now.) (y/n): y
Job was scheduled 8: [Interval: 00:00:60 Mask: * * * * *] rulesMonitor sms none smsPppOn 60
```

The sequence for this feature is:

1.	Monitor runs checks for new messages.
2.	If there are new messages, they are parsed and decrypted. Only properly encrypted messages (those sent from the Control Center) will be captured. An alarm will be generated if the message is not properly encrypted.
3.	The smsPppOn rule is applied to captured commands. Currently, the only valid command is *pppOn*. 
4.	If the sms command is *pppOn*, the appliance performs the pppOn action.

The smsPppOn rule is basic:

```
[admin@UplogixLM]# show rule smsPppOn
rule smsPppOn
action pppOn
conditions
sms.command equals pppOn
exit
exit
```

The rule can be edited to generate alerts or take additional actions.

> The sms monitor must be running for this feature to work.

# A Note About Timing

After clicking Schedule on the Control Center, the instruction to activate PPP must pass through your specified SMTP server, Iridium's E-mail to SMS gateway, and the Iridium network. Once it is delivered, the sms monitor may not run for an additional thirty seconds. After PPP is activated, an out of band path will be created. Once a route is available to the Control Center, it may be an additional thirty seconds before the appliance heartbeats. 