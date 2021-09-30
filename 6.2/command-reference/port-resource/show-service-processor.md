<!-- 5.4 -->

Displays the selected information about the service processor.

# Command availability 

CLI resource: port

Device makes: HP, Sun, server

Uplogix Local Managers: All

LMS offerings: Advanced

# Syntax 

```
show service-processor <config | events | info | power | sensor>
```

# Usage 

**config** - Lists the current configuration of the service processor.

```
[admin@UplogixLM (port1/1)]# show service-processor config
Service processor enabled: true 
Using dedicated ethernet 
IPMI Port: 623 
Username: xyz123
Password: ********
Connection Type: auto(2.0)
```

**events** - Displays the service processor log.

```
[admin@UplogixLM (port1/1)]# show service-processor events
01/16/08 22:06:07.576 - Event Logging Disabled #0x72 | Log area reset/cleared - Asserted
01/16/08 22:06:37.624 - Event Logging Disabled #0x72 | Log area reset/cleared - Asserted
01/16/08 22:07:07.703 - Event Logging Disabled #0x72 | Log area reset/cleared - Asserted
(output removed)
```

**info** - Displays information about the service processor.

```
[admin@UplogixLM (port1/1)]# show service-processor info
Device ID                 : 32
Device Revision           : 0
Firmware Revision         : 1.14
IPMI Version              : 2.0
Manufacturer ID           : 674
Manufacturer Name         : Unknown (0x2a2)
Product ID                : 256 (0x0100)
Device Available          : yes
Provides Device SDRs      : yes
Additional Device Support :
Sensor Device
SDR Repository Device
SEL Device
FRU Inventory Device
IPMB Event Receiver
Bridge
Chassis Device
Aux Firmware Rev Info     :
0x00
0x00
0x00
0x00
```

**power** - States whether the service processor is powered on.

```
[admin@UplogixLM (port1/1)]# show service-processor power 
Chassis Power is on
```
**sensor** - Displays information from the service processor's sensors to give a low-level view of the server's health.

```
[admin@UplogixLM (port1/1)]# show service-processor sensor
Temp             | -47 degrees C     | ok
Temp             | -45 degrees C     | ok
Temp             | 40 degrees C      | ok
Temp             | 40 degrees C      | ok
Ambient Temp     | 22 degrees C      | ok
CMOS Battery     | 0x00              | ok
ROMB Battery     | 0x00              | ok
VCORE            | 0x01              | ok
VCORE            | 0x01              | ok
CPU VTT          | 0x01              | ok
1.5V PG          | 0x01              | ok
1.8V PG          | 0x01              | ok
3.3V PG          | 0x01              | ok
5V PG            | 0x01              | ok
(output removed)
```

# History 

3.4 - This command was introduced.

# Related commands

- **config service-processor**
