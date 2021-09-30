<!-- 5.4 -->

Opens an editor to configure modem behavior. The terminal type must be ANSI and operates like the Uplogix Local Manager's console port. The modem's default configuration is for North America.

# Command availability

CLI resource: modem

Modem: All

Uplogix system: All

LMS offerings: All

# Syntax 

```
config answer
```

# Subcommands 

**show** - display current settings.

**enable** and **disable** - to enable/disable the dial-in feature.

> **Note**: If you use the pulse subcommand to enable the modem to answer on Pulse failure, the modem will do so whether you have applied the enable subcommand or not.

**init <modem init string>** - edit the init string to add country code and other telco variables. 

For example, to enable the modem to be used in Belgium, add the AT+GCI=fd variable to the init string.

To remove a setting, place the **no** modifier before it.

**[no] allow <"phone number" | all>** - allow access from a specific calling phone number or from all numbers. The "phone number" string may be all or part of a phone number.

**[no] deny <"phone number" | all>** - deny access to a specific calling phone number or from all numbers. The "phone number" string may be all or part of a phone number.

**[no] rings <n>** -  answer after (default 2) rings

**[no] ringback <n>** - answers only when a number calls, hangs up, and redials within n seconds. The default is 30 seconds.

**[no] pulse** - Specify whether the modem answers after a Pulse failure initiates outband operation, applying all other defined restrictions. Setting pulse overrides the no enable and disable subcommands.

**[no] suspend** - disable SLV tests when PPP is enabled.

**[no] logrings** - Enable inbound call attempts

**[no] number <Local Manager phone number>** and **[no] domain <SMS domain name>** - these are both used in constructing the SMS email address that Uplogix Control Center uses when sending the ppp on message to establish contact with an Uplogix Local Manager at a remote location. This capability is available for cellular and Iridium modems.

**show** - display current settings

**exit** - leave the modem configuration editor.

# Usage 

By default, the modem is not in auto-answer mode - all calls are ignored.

Caller ID can be used to accept (**allow**) or refuse (**deny**) calls. Caller ID information is transmitted between the first and second rings. The **allow** and **deny** commands use whole prefix masking, for example allowing all numbers within a specific area code, denying numbers beginning with a specified string of digits, or allowing specific numbers such as 4045551212. In the example below, calls from the phone number 2128675309 are allowed but all calls that begin with the string 512471 are blocked. 

The following example shows a basic configuration:

```
[admin@UplogixLM (modem)]# config answer
[config answer]# enable
[config answer]# init "" ATZ
[config answer]# allow all
[config answer]# exit
```
This example shows a more complex configuration:

```
[admin@UplogixLM (modem)]# config answer
[config answer]# enable
[config answer]# rings 5
[config answer]# allow 2128675309
[config answer]# deny 512471
[config answer]# ringback 30
[config answer]# pulse
[config answer]# suspend
[config answer]# logrings
[config answer]# number 512-555-1212
[config answer]# domain mobile.att.net
[config answer]# init "" ddd+++dddATS0=0&S1 OK AT+VCID=1 OK AT+GCI=fd
```

> **Note**: Be sure to include the double quotes in the init string. 
 
# In the Uplogix web interface

**Inventory > group page > Out-of-Band > Modem** - specific to this inventory group

**Inventory > Local Manager page > Out-of-Band > Modem** - specific to this modem

# History 

2.5 - This command was introduced. It replaces config Local Manager modem.

3.3 - Subcommands domain and number were added to support Iridium modem.

4.1 - Log Rings command added to record inbound dial attempts.

# Related commands 
 
- **show answer**
