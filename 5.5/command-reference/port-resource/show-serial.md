<!-- 5.4 -->

Displays the deviceâ€™s serial console settings and current statistics. To display the Uplogix Local Managerâ€™s console port parameters, use the **show system serial** command.

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: All

Modem: All

Power controllers: All

Uplogix system: All

LMS offerings: All

# Syntax 

```
show serial
```

# Usage 

```
[admin@UplogixLM (port1/1)]# show serial
Serial Bit Rate: 9,600
Serial Data Bit: 8
Serial Parity: none
Serial Stop Bit: 1
Serial Flow Control: none
DSR: false
CTS: false
Serial Detect: false
RX : 0
TX : 1,471,322
Frame Errors: 0
Overrun Errors: 0
Parity Errors: 0
Breaks: 0

```
#History 

1.1 - Current console statistics added.

#Related commands 

**config serial**
**config system serial**
**show system serial**
