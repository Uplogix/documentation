# Overview

In environments where Local Managers contact the Control Center as needed via satellite modem, you can initiate contact from the Control Center by sending an SMS message instructing an Local Manager to start PPP.

Requirements for using this capability are:

* The Local Manager uses a GSM cellular modem or an Iridium modem.
* The Local Manager has been configured with a phone number and SMS domain name. These are configured with the **config answer** command.
* An SMS modem monitor has been configured on the modem with the smsPppOn rule that tells the Local Manager to initiate the PPP connection when a valid SMS message is received.
* The Control Center must be configured to send email. (Administration / Server Settings / Mail Settings)

# Configure Number and Domain Settings

Using the **config answer** editor, set the Local Managerâ€™s phone number with the **number** subcommand, and use the **domain** subcommand to set the service providerâ€™s SMS domain name. The Uplogix Control Center uses these parameters to construct a valid SMS email address, to which it can send the **ppp on** message to establish contact.

## Iridium Example

```
[admin@UplogixLM (modem)]# config answer
[config answer]# number 881652318392
[config answer]# domain msg.iridium.com
[config answer]# exit
```

## AT&T Example

```
[admin@UplogixLM (modem)]# config answer
[config answer]# number 5125551234
[config answer]# domain txt.att.net
[config answer]# exit
```

# Schedule SMS Monitor
<div class='ucc' />Inventory > Local Manager Summary >Â Schedule</div>

To activate PPP when an SMS message is received, the Local Manager must be configured to check for messages. This can be accomplished with the **config monitor sms** command and the built-in smsPppOn rule.

```
[admin@UplogixLM (modem)]# config monitor sms smsPppOn :60
Validate scheduled monitor(sms)? (This will execute the job now.) (y/n): y
Job was scheduled 8: [Interval: 00:00:60 Mask: * * * * *] rulesMonitor sms none smsPppOn 60
```

The sequence for this feature is:

1. Monitor checks for new messages at specified interval.
2. If there are new messages, they are parsed and decrypted. Only properly encrypted messages (those sent from the Control Center) will be captured. An alarm will be generated if the message is not properly encrypted.
3. The smsPppOn rule is applied to captured commands. Currently, the only valid command is pppOn.
4. If the sms command is pppOn , the appliance performs the pppOn action.

The smsPppOn rule consists of:

```
[admin@UplogixLM]# show rule smsPppOn
rule smsPppOn
action pppOn
conditions
sms.command equals pppOn
exit
exit
```

It can be edited to generate alerts or take additional actions.

> The SMS monitor must be running for the SMS-initiated PPP feature to work.

# Activate PPP via SMS
Once the Local Manager has been configured, you can initiate a PPP connection by scheduling an â€œSMS Messageâ€ task from the Local Manager Summary page on the Control Center. The message will need to be delivered via email, turned into an SMS message, received by the Iridium modem, and noticed by the Local Manager before the PPP connection will be turned on. It may take an additional 30 seconds for heartbeats to resume over the out-of-band link.