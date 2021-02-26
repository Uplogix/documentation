<!-- 5.4 -->

Manages power from the device's perspective. The power controller must have been previously configured. Multiple outlets are supported to facilitate devices with multiple power supplies. 

Following **power cycle**, the device is checked against a number of measures to assure power cycle was a success. Following **power off**, console status is checked to make sure device has completely shut down, identified by console electrical signals. Following **power cycle** or **power on**, POST (Power On Self Test) takes up to five minutes to time-out if an error has occurred.

Rules can be defined to automate this operation using the powerCycle, powerOff, and powerOn actions.

# Command availability

CLI resource: port, modem

Device makes: All

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
power <on | off | cycle [â€œdelayâ€]>
```

The optional delay is in seconds.

# Usage 

```
[admin@UplogixLM (port1/1)]# power cycle
Powering off outlet(s) [1, 2]
DSR was active.
CTS was active.
CTS is still active.
Powering on outlet(s) [1, 2]
Serial link is active.
Reading post
Image decompressed
Device loaded
Post complete.
```
```
[admin@UplogixLM (port1/1)]# power on
Powering on outlet(s) [1, 2]
Serial link is active.
Reading post
Device loaded
Post complete.
```

During a terminal pass-through session, you can use the **~p** command in the same way.

# History 
--

# Related commands 

- **on**
- **off**
