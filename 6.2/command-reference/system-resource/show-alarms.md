<!-- 5.4 -->

Displays information about current and recent alarms.

Time is offset by user's time zone offset, listed as common abbreviation (such as CDT, US Central Daylight Saving Time) or relative to UTC. Alarms lasting a day are listed as their date.

Once an alarm triggers, it silences automatically in 6 minutes. An asterisk denotes no alarm in the past 2 minutes.

Alarms remain on the Uplogix Local Manager as space permits. Alarms are archived on the Uplogix Control Center (Management Server) if one is used.

# Command availability 

CLI resource: All

Device makes: All

Modem: All

Power controllers: All

Uplogix system : All

LMS offerings: All

# Syntax 

```
show alarms [-all | -cleared | -n | -v]
```

**-all** - displays alarms that are no longer current but have not been rolled off
**-v** - displays detailed alarms information
**-cleared** - display alarms that have already been cleared
**-n [#]** - display up to the specified number of alarms

# Usage 

```
[admin@UplogixLM]# show alarms
GMT    Elapsed  Device  Context  Message
-----  -------  ------  -------  --------------------------------------------------------------------------
09/19  0:33                       Archive failed. (Could not put file [403]: Forbidden)
09/19  0:00                       System and management server clocks are more than 20 seconds out of sync.
09/19  0:00                       NTP server invalid. ('198.51.51.20', server strata too high)
08/21  0:11                       Failed to connect to pulse server. (198.51.12.31:7)


```
```
[admin@UplogixLM]# show alarms -v
-------------------------------------------------------------------------------
[Current]                       Elapsed: 0:28
Start: 2017-09-19 16:00 GMT     Duration:  508:59:04              Count: 35951
Description: Archive failed. (Could not put file [403]: Forbidden)
-------------------------------------------------------------------------------
[Current]                       Elapsed: 0:08
Start: 2017-09-19 15:59 GMT     Duration:  509:00:59              Count: 57623
Description: System and management server clocks are more than 20 seconds out of sync.
-------------------------------------------------------------------------------
[Current]                       Elapsed: 0:08
Start: 2017-09-19 15:59 GMT     Duration:  509:01:04              Count: 116681
Description: NTP server invalid. ('198.51.51.20', server strata too high)
-------------------------------------------------------------------------------
[Current]                       Elapsed: 0:29
Start: 2017-08-21 12:35 GMT     Duration:  1208:24:37             Count: 96740
Description: Failed to connect to pulse server. (198.51.12.31:7)
-------------------------------------------------------------------------------
```

# In the Uplogix web interface

**Alarms** - entire inventory

**Inventory > Local Manager page > Alarms** - specific to this system


**Inventory > Local Manager page > port detail > Alarms** - specific to this device

# History 

1.04 - Added port level command to display filtered by port.

1.1 - Alarm duration tracked individually; alarms stored for review.

# Related commands 

- **show events**
