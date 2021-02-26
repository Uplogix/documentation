When a connected device is initialized as hp, sun, or server using the **config init** command, the service processor commands become available to help automate server management.

# Configuring the service processor

Use the **config service-processor** command to configure communication with the service processor.

```
[admin@UplogixLM (port1/2)]# config service-processor
Service processor enabled: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Enable service processor (y/n) [n]: y
Service processor host IP: 10.10.10.2
Service processor IPMI port [623]:
Service processor username: solar2
Service processor password: ********
Confirm Password: ********
Service processor connection type [auto]:
Do you want to commit these changes? (y/n): y
```

# Viewing service processor information

Use the show service-processor commands to view information about the service processor:

**show service-processor config** â€” Lists the current configuration of the service processor.

**show service-processor events** â€” Displays the service processor log.

**show service-processor info** â€” Displays information about the service processor.

**show service-processor power** â€” States whether the service processor is powered on.

**show service-processor sensor** â€” Displays information from the service processor's sensors to give a low-level view of the server's health.

# Working with the service processor using IPMI

Use the **service-processor execute** command to work directly with the service processor. 

Command syntax is: **service-processor execute [command]**

[command] may be any of these:

***Channel*** - Configure Management Controller channels

***Chassis*** - Get chassis status and set power state

***Event*** - Send pre-defined events to Management Controller

***Fru*** - Print built-in FRU and scan SDR for FRU locators

***Fwum*** - Update IPMC using Kontron OEM Firmware Update Manager

***i2c*** - Send an I2C Master Write-Read command and print response

***isol*** - Configure IPMIv1.5 Serial-over-LAN

***kontronoem*** - OEM commands for Kontron devices

***lan*** - Configure LAN channels

***mc*** - Management Controller status and global enables

***pef*** - Configure Platform Event Filtering (PEF)

***picmg*** - Run a PICMG/ATCA).

***power*** - Shortcut to chassis power commands

***raw*** - Send a RAW IPMI request and print response

***sdr*** - Display Sensor Data Repository entries and readings

***sel*** - Display System Event Log (SEL)

***sensor*** - Display detailed sensor information

***session*** - Display session information

***sunoem*** - OEM commands for Sun servers

***user*** - Configure Management Controller users

# Controlling power to the service processor

Use the **service-processor power** command to control power to the service processor. Command parameters are on, off, and cycle.