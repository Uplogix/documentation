<!-- 5.4 -->

Suspends automatic interaction processes, including rules engine, automated jobs, automated recovery procedures, and (from the system context) heartbeat.

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Foundry, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sea Tel, Sun, Tasman, TippingPoint, ppp, server

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

System:

```
suspend < off | on > [-duration {0..120}]
```
Modem, Port: 
```
suspend < off | all | automated | recovery > [-duration {0..120}] 
```

- **all** â€“ Suspends all data collection and automated processes for the port.
- **automated** â€“ Suspends all but recovery-oriented processes such as configuration rollback and ROMmon detection.
- **recovery** â€“ Suspends only automated recovery and config rollback. Data collection and alerting will continue 
- **-duration** â€“ Set the suspend duration in minutes. Default is 60 minutes.

# Usage  

```
[admin@UplogixLM]# suspend
Local Manager automated operations suspended for 60 minutes
```
```
[admin@UplogixLM (port1/1)]# suspend recovery -duration 100
port1/1 is suspended for 100 minutes.
All recovery operations are suspended: rommon, config recovery, etc.
Terminal pass-through configuration rollback is suspended.
```
```
[admin@UplogixLM (port1/1)]# suspend
port1/1 is suspended for 60 minutes.
All scheduled jobs are suspended.  Log collection is suspended.
```
To resume normal operations before the suspend command times out, use the suspend command to reset the suspend duration - for example, **suspend -duration 1** causes normal operation to resume after one minute.

# History 

1.1 - Port level suspend was added.

# Related commands 
--
