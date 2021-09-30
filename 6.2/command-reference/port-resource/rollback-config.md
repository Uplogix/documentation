<!-- 5.4 -->

Undo the last change to the device's configuration.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, Comtech EF Data, Garmin, iDirect, Juniper, 
Netscreen, Tasman

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
rollback config
```

# Usage 

```
[admin@UplogixLM (port1/1)]# rollback config
Retrieving running-config from device ...
Complete. running-config pulled.
Transferring via XModem. (Attempt 1)
Initiating file transfer
Transferring file ...
Sent running-config-undo40011.img at 133 B/s.
File running-config-undo40011.img was transferred to the device successfully via XModem.
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
Rollback successful.
running 'write memory'
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
```

# History 
--

# Related commands 

- **show rollback-config**
