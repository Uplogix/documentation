<!-- 5.4 -->

Display recent events on this resource. Events are single occurrences that do not have durations.

# Command availability 

CLI resource: system, port, modem

Device makes: All

Modem: All

Uplogix system: All

LMS offerings: All

# Syntax 

```
show events [-g] [-n <#>] [-v]
```

**-g** â€“ Show latitude and longitude (only available on ports connected to supported GPS devices).
**-n <#>** â€“ Specify maximum number of events.
**-v** â€“ Use multiple lines

# Usage 

```
[admin@UplogixLM]# show events
UTC   Context              Message
----- -------------------- --------------------------------------------------
07/02 admin@198.51.235.145 User completed a terminal session. (No changes were
07/02 admin@198.51.235.145 User completed a terminal session with changes.
07/02 admin@198.51.235.145 User logged out of Local Manager. (Local Manager detected user session
02:41 tasman-6300-ds3      Pull running config completed.
02:41 tasman-6300-ds3      Pull startup config completed.
05:41 tasman-6300-ds3      Pull running config failed.
05:41 tasman-6300-ds3      Pull startup config completed.
08:41 tasman-6300-ds3      Pull running config completed.
08:41 tasman-6300-ds3      Pull startup config failed.
11:41 tasman-6300-ds3      Pull running config completed.
11:41 tasman-6300-ds3      Pull startup config completed.
14:41 tasman-6300-ds3      Pull running config completed.
14:41 tasman-6300-ds3      Pull startup config completed.
15:20 admin@198.51.235.149 User logged into Local Manager.
```

# In the Uplogix web interface

**Inventory > Local Manager page > Events** - specific to this system

**Inventory > Local Manager page > port detail > Events** - specific to this device

# History 
--
# Related commands 

- **show gps events**
- **show log event**
