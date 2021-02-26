<!-- 5.4 -->

Displays basic diagnostic information for Comtech EF Data and Sea Tel devices.

# Command availability 

CLI resource: port

Device makes: Comtech EF Data, Sea Tel

Uplogix Local Managers: All 

LMS offerings: All

# Syntax 

```
show faults [-v]
```
For more detailed information on system faults, use the verbose option (**-v**) on the show faults command. The verbose command will display the DAC status words and their translation.

# Usage 

```
[admin@UplogixLM (port1/3)]# show faults
PCU Status Bit 0, Satellite out of range, PCU Error, AZ Reference Error, Polang Drive Off, Band Tone Off, Band 13V, AUX is off, Band C, Local-RF 18V, Local Tone Off, No Force NID, FEC-SCPC
```
```
[admin@UplogixLM (port1/3)]# show faults -v
   Word 1: 0x40 (01000000)  64 '@'
   Word 2: 0x40 (01000000)  64 '@'
   Word 3: 0x68 (01101000) 104 'h'
   Word 4: 0x48 (01001000)  72 'H'
Remote RF: 0x40 (01000000)  64 '@'
 Local RF: 0x67 (01100111) 103 'g'
    TDisp: 0x00 (00000000)   0 '\u0000'
Satellite out of range, PCU Error, AZ Reference Error, Polang Drive Off, Band Tone Off, Band 13V, AUX is off, Band C, Local-RF 18V, Local Tone Off, No Force NID, FEC-SCPC
```
# History 

3.5 - This command was introduced.

# Related commands
--
