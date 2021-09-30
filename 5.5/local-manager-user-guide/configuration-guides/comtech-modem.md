*Written for RMOS 4.3 - October 2010*

# Overview

The purpose of this guide is to describe the procedures for installing and configuring Comtech EF data satellite modems for use with all Uplogix appliances. 

# Supported Models

The Uplogix RMOS revision 4.3 includes support for the following Comtech EF Data Satellite Modems 

* CDM-550
* CDM-570/L
* CDM-570/L-IP
* CDM-570/L-IPEN
* CDM-625

# Physical Installation

The Remote Control (RS232) port of the Comtech modem will be connected to the Uplogix appliance using a DB-9 -> RJ-45 adapter. Connect the adapter to a serial port on the appliance using standard CAT5 cable. If you are using a 430, you will need a rolled cable.

# Enabling Serial Remote Mode

In order for the Uplogix appliance to manage the Comtech EF Data satellite modem, the modem must be in Serial Remote Mode. Both Local Mode and Ethernet Remote Mode are unsupported.

From a configured port:

```
[admin@UplogixLM (port1/2)]# device execute LRS=1
```

From the terminal:

```
<0000/LRS=1
```

From the editor:

```
[admin@UplogixLM (port1/2)]# edit run current
[comtech] Local = Serial Remote
[comtech] exit
saving config as candidate ...

[admin@UplogixLM (port1/2)]# push run candidate
pushing running-config ...
running-config saved to archive as current.
```

# Configuring the Comtech EF Data satellite modem

Use a workstation to open a terminal or SSH session to the Uplogix appliance. 

Issue the **port** command to switch to the appropriate port:

```
[admin@UplogixLM]# port1/2	{use the port that your Comtech modem is connected to} 
native

[admin@UplogixLM (port1/2)]#
``` 

Use the **config init** command to configure the satellite modem. 

```
[admin@UplogixLM (port1/2)]# config init 
--- Enter New Values --- 
description: []: Comtech
make: [embedded]: Comtech 
model: CDM 550	{enter your device type- CDM 550, CDM 570, or CDM 625}
os: []:
os version: []:
management IP: []:
configure dedicated ethernet port? (y/n) [n]:
console username: []:
console password []:
enable username: []:
enable password []:
serial bit rate [38400]: 9600 
serial data bit [8]: 
serial parity [none]: 
serial stop bit [1]: 
serial flow control [none]: 
use null modem (rolled cable to device)? (y/n): n
Do you want to commit these changes? (y/n): y 
```

Issue the **terminal** command to start a terminal session with the modem.

``` 
[admin@UplogixLM (port1/2)]# terminal 
Press ~[ENTER] to exit 
Connecting ... 
Console session started.
```
 
Issue the <0/TFT? command to verify communication with the modem. You should see the following response: 

```
<0/TFT?
>0000/TFT=2
```

# Editing Comtech Configurations

To begin working with the Configuration Editor, navigate to the configured Comtech port and enter the command: 

```
[admin@UplogixLM (port1/2)]# edit running-config <option>
```

In this instance, we've elected to edit the current configuration. However, you can choose to edit the previous configuration or any of the archive configurations stored on the Uplogix appliance with the same command. 

```
[admin@UplogixLM (port1/2)]# edit running-config ?
edit running-config <candidate | current | previous | archive #>
```

# Editor Help
Within the editor, using the ? will provide a list of the available commands.

``` 
[comtech] ?
<parameter>	- displays parameter information and its current value
<parameter> = <value> - sets parameter to value enclose value in quotes ('' or "") to preserve spaces
show		- shows current configuration
exit		- exits shell, saving config as candidate if changed
Modem configuration parameters can be accessed using the three letter Comtech EF Data command or via the description. Entering a partial description will result in a list of matching parameters
[comtech] tx
similar parameters:
Tx Interface Type
Tx Framing Mode
Tx FEC Type
Tx Modulation Type
Tx FEC Code Rate
Tx Sub-Mux on/off
Tx Sub-Mux Ratio
Tx Data Invert
Tx Reed-Solomon Encoding
Tx Spectrum Invert
Tx Scrambler
Tx Carrier State
Tx Clock Source
Tx Clock Invert
Tx Ternary Code
Tx BERT State
Tx BERT Pattern
Tx Frequency
Tx Power Level
Tx Data Rate
Tx Audio Volume Control
Tx Drop Timeslot
Tx LO Frequency

[comtech] tx fec
similar parameters:
Tx FEC Type
Tx FEC Code Rate
```

Entering the full parameter name without value will display the possible parameter values and help information if there is any available. For example: 

```
[comtech] tx fec code rate
&#35;  Parameter: Tx FEC Code Rate
&#35; Tx FEC Code Rate, where
&#35; 0=Rate 1/2
&#35; 1=Rate 3/4
&#35; 2=Rate 7/8
&#35; 3=Rate 2/3 (8-PSK TCM or LDPC only)
&#35; 4=Rate 1/1 (Uncoded or No FEC)
&#35; 5=Rate 21/44 (Turbo Only)
&#35; 6=Rate 5/16 (Turbo Only)
&#35; 7=Rate 0.95 (Turbo Only) (aka 17/18)
&#35; A=VersaFEC CCM ModCode 0 - BPSK 0.488
&#35; B=VersaFEC CCM ModCode 1 - QPSK 0.533
&#35; C=VersaFEC CCM ModCode 2 - QPSK 0.631
&#35; D=VersaFEC CCM ModCode 3 - QPSK 0.706
&#35; E=VersaFEC CCM ModCode 4 - QPSK 0.803
&#35; F=VersaFEC CCM ModCode 5 - 8-QAM 0.642
&#35; G=VersaFEC CCM ModCode 6 - 8-QAM 0.711
&#35; H=VersaFEC CCM ModCode 7 - 8-QAM 0.780
&#35; I=VersaFEC CCM ModCode 8 - 16-QAM 0.731
&#35; J=VersaFEC CCM ModCode 9 - 16-QAM 0.780
&#35; K=VersaFEC CCM ModCode 10 - 16-QAM 0.829
&#35; L=VersaFEC CCM ModCode 11 - 16-QAM 0.853
&#35; Depending on FEC type, not all of these selections will be valid
&#35; Example: TCR=1 (which is Rate 3/4)
Tx FEC Code Rate=Rate 1/1 (Uncoded or No FEC)
```

Help text is specific to modem type. Entering the name of a parameter that does not exist will result in a "no such parameter" response.

```
[comtech] alpha?
no such parameter
```

# Setting Parameter Values

To set the value, enter the parameter name with value as shown in the example below:

```
[comtech] tx fec code rate=1
The TX FEC Rate has now been set to 3/4.
```

If a user attempts to set a parameter to a value not possible for the parameter, the appliance will respond with "Invalid input value", display the set of possible parameter values and the current parameter value. In the example below, the user attempted to set the TX FEC Code Rate to 8 which is not a possible value for this parameter. 

```
[comtech] tx fec code rate=8
Invalid input value: 8
&#35;  Parameter: Tx FEC Code Rate
&#35; Tx FEC Code Rate, where
&#35; 0=Rate 1/2
&#35; 1=Rate 3/4
&#35; 2=Rate 7/8
&#35; 3=Rate 2/3 (8-PSK TCM or LDPC only)
&#35; 4=Rate 1/1 (Uncoded or No FEC)
&#35; 5=Rate 21/44 (Turbo Only)
&#35; 6=Rate 5/16 (Turbo Only)
&#35; 7=Rate 0.95 (Turbo Only) (aka 17/18)
&#35; A=VersaFEC CCM ModCode 0 - BPSK 0.488
&#35; B=VersaFEC CCM ModCode 1 - QPSK 0.533
&#35; C=VersaFEC CCM ModCode 2 - QPSK 0.631
&#35; D=VersaFEC CCM ModCode 3 - QPSK 0.706
&#35; E=VersaFEC CCM ModCode 4 - QPSK 0.803
&#35; F=VersaFEC CCM ModCode 5 - 8-QAM 0.642
&#35; G=VersaFEC CCM ModCode 6 - 8-QAM 0.711
&#35; H=VersaFEC CCM ModCode 7 - 8-QAM 0.780
&#35; I=VersaFEC CCM ModCode 8 - 16-QAM 0.731
&#35; J=VersaFEC CCM ModCode 9 - 16-QAM 0.780
&#35; K=VersaFEC CCM ModCode 10 - 16-QAM 0.829
&#35; L=VersaFEC CCM ModCode 11 - 16-QAM 0.853
&#35; Depending on FEC type, not all of these selections will be valid
&#35; Example: TCR=1 (which is Rate 3/4)
Tx FEC Code Rate=Rate 1/1 (Uncoded or No FEC)
```

# Exiting the Editor

Type **exit** to leave the Configuration Editor. Upon exit you will notice the configuration you edited is now saved as candidate.

```
[comtech] exit
saving config as candidate ...
```

# Device execute
The **device execute** command allows Comtech commands to pass directly from the port command line to the modem. Using the device execute command will make changes to the current running configuration on the modem. The Uplogix appliance will archive the current version of the configuration prior to p. The current version is archived in case the command places the modem in a bad state which would require a configuration rollback.

## Using Device Execute
To change parameter values using device execute, enter the three letter Comtech command and the new value:

```
[admin@UplogixLM (port1/2)]# device execute EBA=02.0
running-config saved to archive as current.
EBA=

[admin@UplogixLM (port1/2)]# device execute EBA?
running-config saved to archive as current.
EBA=02.0
```

In the example above you can see the Eb/No Alarm Point value has been changed to 2.0. When entering commands using device execute, the command must be in the format specified in the Comtech manual. Device execute does not correct parameter formatting like the Configuration Editor does. For example setting the CID parameter requires 24 characters to work correctly - also note to end the CID command with spaces the whole command must be surrounded by quotes:

```
[admin@UplogixLM (port1/2)]# device execute "CID=COMTECH TEST      "
```

## Querying Parameter Values with Device Execute

To query the current value of a Comtech parameter, follow the three letter Comtech command with a ? as in the example below:

```
[admin@UplogixLM (port1/2)]# device execute EBA?
running-config saved to archive as current.
EBA=01.9
```

# Pushing Candidate Configurations to the Comtech Modem

To push a candidate file to the modem, begin by reviewing the configuration to ensure all parameters are set correctly using the **show running-config** command. This command displays the device's current configuration. Using the -t extension displays the configuration in a terse format.

```
[admin@UplogixLM (port1/2)]# show running-config candidate -t
Tx Interface Type = RS422
Tx Framing Mode = Unframed
Tx FEC Type = None (uncoded) with differential enconding ON
Tx Modulation Type = QPSK
Tx FEC Code Rate = Rate 1/1 (Uncoded or No FEC)
Tx Sub-Mux on/off = Off
Tx Sub-Mux Ratio = 1/9
Tx Data Invert = Normal
Tx Reed-Solomon Encoding = Normal (based on the Open Network framing selected)
Tx Spectrum Invert = Normal
Tx Scrambler = Normal
Tx Carrier State = OFF due to front panel or remote control command
Power Level Mode = MANUAL mode (AUPC disabled).
Tx Clock Source = Internal
Tx Clock Invert = Normal
Transmit Terrestrial Alarm Mask = Alarm is masked.
Drop Type = T1-D4
Tx Ternary Code = B8ZS
Transmit Backward Alarms Enable = 0000
Transmit ESC Type = 64k data channel
Rx Interface Type = RS422
Rx Framing Mode = Unframed
Rx FEC Type = Viterbi
Rx Modulation Type = QPSK
Rx FEC Code Rate = Rate 1/2
Rx Sub-Mux on/off = Off
Rx Sub-Mux Ratio = 1/9
Rx Data Invert = Normal
Rx Reed-Solomon Decoding = Normal (based on the Open Network framing selected)
Rx Spectrum Invert = Normal
Rx Descrambler = Normal
Rx Clock Source = Rc Satellite
Rx Clock Invert = Normal
Receive Terrestrial Alarm Enable = Disables the alarm
Insert Type = T1-D4
Rx Ternary Code = B8ZS
Receive Backward Alarms Enable = 0000
Receive ESC Type = 64k data channel
Receive Equalizer Enable = disabled
Local/Remote Status = Serial Remote (RS-232/RS-485)
EDMAC Framing Mode = EDMAC OFF (Idle Mode)
Engineering Service Channel = Disable the high-rate ESC
External Frequency Reference = Internal 10 MHz (default)
Warm-up Delay = Delay off (instant on)
Unit Test Mode = Normal Mode (no test)
Attach a summary LNB fault to the Rx FLT status = Tx FLT status unaffected by LNB fault)
Outdoor Unit Comms enable = Disabled
1:N (One For N) control = Disabled
Request to Send = RTS/CTS Loop, No Action. RTS and CTS are looped, so that CTS echoes the state
of RTS, but RTS does not control the ON/OFF state of the carrier
HSSI Handshake Control = TA to CA loop (default)
POCO feature (Power-On Carrier-Off) = POCO disabled (normal operation)
DoubleTalk Carrier-in-Carrier (CnC) Mode = Off
DoubleTalk Carrier-in-Carrier (CnC) PMSI Mode = Idle
Tx BERT State = Off
Rx BERT State = Off
Tx BERT Pattern = 2047 (default)
Rx BERT Pattern = 2047 (default)
BERT 10E-3 Error Insert = Off
BUC Power Supply enable = Disable the BUC DC Power Supply
BUC 10 MHz Reference = Off
BUC Output Power Enable = Off
LNB DC Power Control = OFF
LNB Reference = Disable LNB Reference
Tx Frequency = 0070.0000
Tx Power Level = 10.0
Rx Frequency = 0070.0000
Eb/No Alarm Point = 00.1
Rx Sweep Width = 010
Rx Buffer Size = 00016
EDMAC Slave Address Range = 0020
Statistics Sampling Interval = 0
CnC Frequency Range/offset = 030
BUC Current Low Limit = 0000
BUC Current High Limit = 2000
BUC Address = 01
LNB Low Current Limit = 000
LNB High Current Limit = 500
Tx Data Rate = 00064.000
AUPC Parameter Setup = 004.03
Tx Audio Volume Control = +0+0
Tx Drop Timeslot = 100000000000000000000000
Tx LO Frequency = 00000-
Rx Data Rate = 00064.000
Rx Audio Volume Control = +0+0
Insert Timeslot = 100000000000000000000000
Rx LO Frequency = 00000-
Circuit ID String = "----------------------------------------"
ESC Parameters = 300
Adjustment for the Internal 10MHz-High-stability Reference = +396
Unit Alarm Mask = 1100100000000
IP Address = 192.001.001.001.24
IP Gateway = 192.001.001.100
Traffic IP Address = 192.168.001.003
CnC Min/Max Search Delay = 010290
G.703 Clock Extension = 00
```

Once you have verified the candidate configuration is acceptable, you are ready to push the candidate file to the modem using the command **push running-config candidate**. The push commands allow you to write a previously saved configuration to a device.

```
[admin@UplogixLM (port1/2)]# push running-config candidate
pushing running-config ...
running-config saved to archive as current.
```

When the file transfer is complete, you can view the new running configuration using the **show running-config current** command. 

```
[admin@UplogixLM (port1/2)]# show running-config current-t
Tx Interface Type = RS422
Tx Framing Mode = Unframed
Tx FEC Type = None (uncoded) with differential enconding ON
Tx Modulation Type = QPSK
Tx FEC Code Rate = Rate 1/1 (Uncoded or No FEC)
Tx Sub-Mux on/off = Off
Tx Sub-Mux Ratio = 1/9
Tx Data Invert = Normal
Tx Reed-Solomon Encoding = Normal (based on the Open Network framing selected)
Tx Spectrum Invert = Normal
Tx Scrambler = Normal
Tx Carrier State = OFF due to front panel or remote control command
Power Level Mode = MANUAL mode (AUPC disabled).
Tx Clock Source = Internal
Tx Clock Invert = Normal
Transmit Terrestrial Alarm Mask = Alarm is masked.
Drop Type = T1-D4
Tx Ternary Code = B8ZS
Transmit Backward Alarms Enable = 0000
Transmit ESC Type = 64k data channel
Rx Interface Type = RS422
Rx Framing Mode = Unframed
Rx FEC Type = Viterbi
Rx Modulation Type = QPSK
-- Output abbreviated in this example -
```

# Rolling Back to a Previous Configuration

If you need to roll back to a previous configuration on the Comtech, first identify the correct configuration. To view a listing of running configurations saved on the appliance run the **show directory** command:

```
[admin@UplogixLM (port1/2)]# show directory
Type   Version  Name
------- --------- ------------
Config
  Running
     Candidate running-config
     Current  running-config
     Previous  running-config
```

You can confirm the configuration you would like to roll back to by reviewing the configuration by running the command **show running-config <configuration name>**. This command displays the device's current configuration. 

```
[admin@UplogixLM (port1/2)]# show running-config previous -t
Tx Interface Type = RS422
Tx Framing Mode = Unframed
Tx FEC Type = None (uncoded) with differential enconding ON
Tx Modulation Type = QPSK
Tx FEC Code Rate = 2/3 (8-PSK TCM or LDPC only)
Tx Sub-Mux on/off = Off
Tx Sub-Mux Ratio = 1/9
Tx Data Invert = Normal
Tx Reed-Solomon Encoding = Normal (based on the Open Network framing selected)
Tx Spectrum Invert = Normal
Tx Scrambler = Normal
Tx Carrier State = OFF due to front panel or remote control command
Power Level Mode = MANUAL mode (AUPC disabled).
Tx Clock Source = Internal
Tx Clock Invert = Normal
Transmit Terrestrial Alarm Mask = Alarm is masked.
Drop Type = T1-D4
Tx Ternary Code = B8ZS
Transmit Backward Alarms Enable = 0000
Transmit ESC Type = 64k data channel
Rx Interface Type = RS422
Rx Framing Mode = Unframed
Rx FEC Type = Viterbi
-- Output abbreviated in this example -
```

Once you have verified the configuration is acceptable, you are ready to push the file to the modem using the command **push running-config <configuration name>**. The push commands allow you to write a previously saved configuration to a device. The example below shows rolling back to the previous configuration version.

```
[admin@UplogixLM (port1/2)]# push running-config previous
pushing running-config ...
running-config saved to archive as current.
```

When the file transfer is complete, you can view the new running configuration using the **show running-config current** command.

``` 
[admin@UplogixLM (port1/2)]# show running-config current
Tx Interface Type = RS422
Tx Framing Mode = Unframed
Tx FEC Type = None (uncoded) with differential enconding ON
Tx Modulation Type = QPSK
Tx FEC Code Rate = 2/3 (8-PSK TCM or LDPC only)
Tx Sub-Mux on/off = Off
Tx Sub-Mux Ratio = 1/9
Tx Data Invert = Normal
Tx Reed-Solomon Encoding = Normal (based on the Open Network framing selected)
Tx Spectrum Invert = Normal
Tx Scrambler = Normal
Tx Carrier State = OFF due to front panel or remote control command
Power Level Mode = MANUAL mode (AUPC disabled).
Tx Clock Source = Internal
Tx Clock Invert = Normal
Transmit Terrestrial Alarm Mask = Alarm is masked.
Drop Type = T1-D4
Tx Ternary Code = B8ZS
Transmit Backward Alarms Enable = 0000
Transmit ESC Type = 64k data channel
Rx Interface Type = RS422
Rx Framing Mode = Unframed
Rx FEC Type = Viterbi
 -- Output abbreviated in this example --
```

For further details and instructions for your Comtech EF Data satellite modem, please consult the manual, which can be found here: [http://www.comtechefdata.com/modemDocs.asp#manuals](http://www.comtechefdata.com/modemDocs.asp#manuals)

# Configuring Uplogix monitors

Uplogix monitors collect chassis and interface data from supported network devices. There are two monitors that have been implemented for the Comtech EF Data modem: chassis and remotestate. Once the modem has been initialized using the **config init** command, these monitors will be created with a 30 second interval. Both monitors can be run with two options: -n <count> to display multiple chronological values, and "-t" which will add an elapsed time value to the results.

```
[admin@UplogixLM (port1/2)]# show chassis -n 4 -t
Time elapsed: 0:21
Temperature: 37.0 degrees

Time elapsed: 0:51
Temperature: 37.0 degrees

Time elapsed: 1:21
Temperature: 37.0 degrees

Time elapsed: 1:51
Temperature: 37.0 degrees

[admin@UplogixLM (port1/2)]# show remotestate
Eb/No: 99.9 dB
Remote Eb/No: -1.0 dB
Transmit Power Level Increase: -1.0 dB
Receive Frequency Offset: 99999.0 kHz
Buffer Fill State: 0 %
Receive Bit Error Ratio: 99999.0
```

Information collected in monitors is available for use with the Uplogix rules engine. The rules engine can be used to create customized rules to evaluate conditions and take actions.