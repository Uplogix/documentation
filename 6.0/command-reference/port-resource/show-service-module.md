<!-- 5.4 -->

Displays collected interface statistics and any carrier alarms on that interface.


# Command availability 

CLI resource: port

Device makes: Cisco

Uplogix system: All

LMS offerings: All

# Syntax 

```
show service-module <â€œinterface nameâ€> [-n <#>]
```
Use the optional **â€“n** parameter with an integer to specify the number of records to display.

#Usage 

Statistical data is purged from the local database based on available storage and is available via export or archive for long term access.

```
[admin@UplogixLM (Port 1/1)]# show service-module Serial0/0
Module type is T1/fractional
    Hardware revision is 0.88, Software revision is 0.2,
    Image checksum is 0x73D70058, Protocol revision is 0.1
Receiver has no alarms
Framing is ESF, Line Code is B8ZS, Current clock source is line,
Fraction has 2 timeslots (64 Kbits/sec each), Net bandwidth is 128 Kbits/sec.
Last clearing of alarm counters null
    loss of signal       :0,
    loss of frame        :0,
    AIS alarm            :0, 
    Remote alarm         :10,
    Module access errors :0,
Data in current interval (602 seconds elapsed):
    0 Line Code Violations, 0  Path Code Violations
    0 Slip Secs, 0 Fr Loss Secs, 0 Line Err Secs,0 Degraded Mins
    0 Errored Secs, 0 Bursty Err Secs, 0 Severely Err Secs, 0 Unavail Secs
```

# History 

1.1 - This command was introduced.

#Related commands 

- **config monitors**
