<!-- 5.4 -->

Displays GPS-tagged event history.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, ppp, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show gps <events | most-recent | position>

```
**events** - Shows GPS coordinates associated with Uplogix events.

**most-recent** - Displays most recent valid GPS coordinates.  Since multiple GPS sources can provide coordinates, the most recent valid coordinate with the port collected is displayed.

**position** - Displays the GPS coordinate history.

# Usage 

```
[admin@UplogixLM (port1/3)]# show gps events
CDT   Latitude          Longitude         Context Message
----- ----------------- ----------------- ------- -----------------------------------------
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Assimilate completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         User started a terminal session.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Pull running config completed.
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation 90 succeeded
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation 0 succeeded
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation 45 succeeded
10/05 30d 22' 00.000" N 97d 46' 00.000" W         Elevation Range Test succeeded
```
```
admin@UplogixLM (port1/3)]# show gps most-recent
Most-recent, port1/1:
CDT        Latitude            Longitude           Heading   Elevation   # Sats
--------   -----------------   -----------------   -------   ---------   ------
15:30:21   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
```
```
[admin@UplogixLM (port1/3)]# show gps position
CDT        Latitude            Longitude           Heading   Elevation   # Sats
--------   -----------------   -----------------   -------   ---------   ------
14:59:46   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:00:24   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:00:46   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:01:23   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:02:01   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:02:24   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:17:51   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:18:13   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
15:18:50   30d 22' 00.000" N   97d 46' 00.000" W       0.0         0.0        1
```
# History 

2.2 - This command was introduced.

# Related commands 
--
