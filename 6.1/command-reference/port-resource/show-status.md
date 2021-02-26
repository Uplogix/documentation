<!-- 5.4 -->

Displays the current device status. The command schedules an interactive collection to gauge the operational state of the device.


# Command availability 

CLI resource: port, modem

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sea Tel, Sun, Tasman, TippingPoint, ppp, server

Modem: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show status
```

# Usage 

If there is a monitor or scheduled job executing, the status command will queue, causing a delay in the return of the status.

```
[admin@UplogixLM (port1/3)]# show status
Waiting for another job to complete
Hostname     : Cat4003
Serial Number: JAE041600WW
Make         : cisco
Model        : WS-C4003
OS Type      : CatOS
OS Version   : 7.6(7)
Uptime       : 3 weeks, 4 days, 5 hours, 47 minutes
```

# History 
--
#Related commands 

- **show dashboard**
