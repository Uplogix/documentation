# Overview

Uplogix Local Managers can be managed by an Uplogix Control Center, a centralized web-based interface for managing multiple systems in an enterprise. Once integrated, the Uplogix Control Center becomes the vehicle for scheduling tasks across the enterprise, archiving data, events and device information, and integrating with other enterprise network management systems.

Local Managers communicate with the Uplogix Control Center server via a "heartbeat" function. The interval is configurable; the default is 30 seconds.

<div class='ucc' />Inventory > Local Manager Summary > Network > Management Server</div>

# Enabling Management

To configure the Local Manager to communicate with an Uplogix Control Center, use the interactive **config system management** command. 

```
[admin@UplogixLM]# config system management
--- Existing  Values ---
Use Management Server: auto
Hostname or IP: (searching)
Port: 
Heartbeat interval (seconds): 30
Heartbeat band: all
Always use minimal heartbeat: false
Last successful heartbeat:  (not yet contacted)
Change these? (y/n) [n]: y
--- Enter New Values ---
Use Management Server (y/n/auto) [auto]: y
Hostname or IP [127.0.0.1]: 10.10.10.25
Set NTP location to 10.10.10.25 (y/n) [n]: y
Port [8443]: 
Heartbeat interval (seconds) [30]: 
Heartbeat during [all]: 
Do you want to commit these changes? (y/n): y
```

Management server settings include:

* **Use Manager Server** - If set to *auto*,  the Local Manager will attempt to discover the address of the Control Center through DNS. Requires DNS and an SRV (service) record name _uplogix._tcp.\* or an A (host) record named *uplogix-control-center*. <!-- Consider adding link to Zero Touch Deployment Overview -->
* **IP** - The IP address of the Control Center. Both IPv4 and IPv6 addresses are supported. Hostnames can be used if a DNS server has been specified in **config system ip** or **config system ipv6**.
* **Port** - The default port is 8443 (as configured on the Control Center).
* **Heartbeat Interval** - The default is 30 seconds. Values from 30 to 604,800 are supported. Higher heartbeat intervals reduce impact to the network and to Control Center resources.
* **Heartbeat during** - Specifies whether to heartbeat while in-band, out of band, or both.
* **Always use minimal heartbeat** - To further reduce network impact, the system can exchange minimal information with the Control Center during heartbeat. This feature is only configurable from the Control Center.

Once you save the settings, the Local Manager will automatically attempt to contact the Control Center. You can view heartbeat status with the **show system management** command. 

```
[admin@UplogixLM]# show system management
Use Management Server: yes
Hostname or IP: 10.10.10.25
Port: 8443
Heartbeat interval (seconds): 30
Heartbeat band: all
Always use minimal heartbeat: false
Last successful heartbeat: 11/01/2020 10:08:34 CDT (Full)
```

The last line of the output shows when the last heartbeat occurred and what kind it was (full vs minimal). If the time is more than 30 seconds (by default) in the past, try running **show alarms** to view any potential heartbeat alarms.

# Archiving

When Control Center management is enabled, the system will begin uploading alarms data via the heartbeat and archive features. Most data transferred via heartbeat is real-time information such as uptime, CPU usage, alarms, and events every 30 seconds. Larger data, such as user sessions and device files, are sent via archive every 60 minutes. Archiving uses high data compression to reduce network impact. 

By default, archives are cached when operating out-of-band or during network failure. 

System configuration can be performed via the CLI or Control Center. If a change is made on the CLI, the new setting will be pushed up to the Control Center during the next heartbeat. Similarly, changes made on the Control Center will transfer down and take effect on the system during the next heartbeat.

To view the system's current archive settings, use the **show system archive** command.

```
[admin@UplogixLM]# show system archive
Time Between Archivals (seconds): 3,600
Maximum Archives Stored Locally: 100
Enable While Out-of-Band: false

```

To edit the system's archive settings, use the **config system archive** command.

```
[admin@UplogixLM]# config system archive
--- Existing  Values ---
Time Between Archivals (seconds): 3,600
Maximum Archives Stored Locally: 100
Enable While Out-of-Band: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Time Between Archivals (300-36000 seconds) [3600]: 1800
Maximum Archives Stored Locally (1-100) [100]:
Enable While Out-of-Band (y/n) [n]:
Do you want to commit these changes? (y/n): y
```

## Clearing Archives

When archives are created, they are tagged with a destination target based on the archive settings at the time of creation. If an archive is generated and destination IP, username, and/or password change before the archive can be transferred to the Control Center, an alarm will be generated indicating the failure. Verifying the correct settings in **config system archive** is not sufficient to clear the alarm; the old (improperly configured) archive must be deleted.

Here is an example of an archive alarm:

```
[admin@UplogixLM]# show alarms 
CDT  Elapsed Device Interface Message 
---- ------- ------ --------- ------------------------------------ 
1/07 2:19                     Archive failed. (connect timed out)
```

To remove old archives, use the **config system clear archive** command.

```
[admin@UplogixLM]# config system clear archive
Remove Queued Archive Files (y/n) [n]: y
Successfully removed queued archive files.
```