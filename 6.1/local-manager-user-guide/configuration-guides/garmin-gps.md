The Uplogix Local Manager supports the Garmin Global Positioning Satellite (GPS) as a standalone device or when included in the Uplogix LEO-I Kit. When a GPS device is installed on the LM, NMEA-183 statements are collected to provide latitude and longitude coordinates for all events and alarms. Automated actions, alerts, and events can be initiated based on GPS data.

This document will cover the installation of the device, how and what data is collected, rule creation, and reporting options.

# Device Configuration

The GPS device is set up just like any LM-supported device. If you are using the LEO-I Kit, please consult its documentation for proper setup. If you are using a standalone Garmin device, you may need to reconfigure the included cable to make it compatible with the LM.

## Serial Cable Pin-out

To connect the Garmin GPS to the LM console port, use the following pin-out (refer to the
Garmin manual for wiring diagram);

```
Garmin     Color    RJ-45
Transmit   White    pin 3
Ground     Black    pin 4
Receive    Blue     pin 6
```

## Initializing the Device

Once the device has been connected, navigate to the proper port and run the **config init**
command.

```
[admin@UplogixLM (port 1/1)]# config init
--- Enter New Values ---
description: []:
make: []: ?
make: []: Garmin
model: []:
os: []:
os version: []:
management IP: []:
configure dedicated ethernet port? (y/n) [n]: n
console username: []:
console password:
enable username: []:
enable password:
serial bit rate [9600]: 4800
serial data bit [8]:
serial parity [none]:
serial stop bit [1]:
Do you want to commit these changes? (y/n): 
```

Note that only the make is required to configure a Garmin GPS. The serial bit rate must be set
at 4800 for proper communication. 

You can verify that initialization was successful by using the **terminal** command to access the
device. NMEA-183 data should be streaming to the console in periods of 1 to 30 seconds.

# Collecting Data

The LM uses monitors to collect GPS data from the device at specified intervals. This data is
stored in the LM's local database and used for events, alarms, and actions as well as longterm
analysis.

# Data Collected

Two NMEA sentences are parsed by the LM. The first is the Recommended Minimum Specific
GPS/TRANSIT Data (RMC). The second is the Global Positioning System Fix Data (GGA). From
these two sentences, the LM collects the following data that can be accessed through the gps
object.

<table>
<thead>
	<tr>
	<th>Field</th>
	<th>Type</th>
	<th>Description</th>
	</tr>
</thead>
<tbody>
<tr><td>gps.status</td><td>char </td><td>A = valid position, V = NAV receiver warning</td></tr>
<tr><td>gps.latitude</td><td> integer </td><td>first 2 characters of latitude field</td></tr>
<tr><td>gps.latitudeMinutes</td><td> double </td><td>remainder of latitude field</td></tr>
<tr><td>gps.latitudeHemisphere</td><td> char </td><td>N or S</td></tr>
<tr><td>gps.normalizedLatitude</td><td> double </td><td>calculated from latitude,
latitudeMinutes, and
latitudeHemisphere.
negative if hemisphere = S</td></tr>
<tr><td>gps.longitude</td><td> integer </td><td>first 3 characters of longitude</td></tr>
<tr><td>gps.longitudeMinutes</td><td> double </td><td>remainder of longitude field</td></tr>
<tr><td>gps.longitudeHemisphere</td><td> char </td><td>E or W</td></tr>
<tr><td>gps.normalizedLongitude</td><td> double </td><td>calculated from longitude, longitudeMinutes, longitudeHemisphere, negative if hemisphere = W</td></tr>
<tr><td>gps.speedOverGround</td><td> double</td><td>Â </td></tr>
<tr><td>gps.courseOverGround</td><td> double</td><td>Â </td></tr>
<tr><td>gps.magneticVariation</td><td> double</td><td>Â </td></tr>
<tr><td>gps.magneticVariationDirection</td><td> char</td><td> E or W</td></tr>
<tr><td>gps.positionFixTime</td><td> date</td><td> calculated from UTC datetime</td></tr>
<tr><td>gps.qualityIndication</td><td> int</td></tr>
<tr><td>gps.numberOfSatellitesInUse</td><td> int</td><td>Â </td></tr>
<tr><td>gps.antennaHeight</td><td> double</td><td>Â </td></tr>
<tr><td>gps.geoidalHeight</td><td> double </td><td>Â </td></tr>
</tbody>
</table>

## Monitoring GPS Data

To collect GPS NMEA data, use the **config monitor gps** command:

```
[admin@UplogixLM (port1/1)]# config monitor gps
Job was scheduled 2: [Interval: 00:05:00 Mask: * * * * *] rulesMonitor gps none 30
```

# Rules

For any value listed in the schema above, rules can be created and used to execute actions.

For example, a simple rule could check to see whether the LM is in the Northern hemisphere.

```
[admin@UplogixLM]# config rule gpsNorth
[config rule gps]# action event -a "IN THE NORTH"
[config rule gps]# conditions
[config rule gps conditions]# gps.latitudeHemisphere equals N 2m
[config rule gps conditions]# exit
[config rule gps]# exit
```

The above example will generate an event whenever the gps.latitudeHemisphere field is equal to
"N" for at least 2 minutes. To schedule a monitor for this rule, use the **config monitor gps**
command:

```
[admin@UplogixLM (port1/1)]# config monitor gps gpsNorth
Job was scheduled 3: [Interval: 00:05:00 Mask: * * * * *] rulesMonitor gps gpsNorth 30
```

# Properties

The LM uses port properties to associate metadata information with the positioning data
collected. Like all ports, properties can define any number of name/value pairs.

For example, to note the installation date of the GPS device, use the following syntax;

```
[admin@UplogixLM (port1/1)]# config system properties
[config properties]# installDate 02-01-06
[config properties]# exit

[admin@LAB1 (port2)]# show prop
installDate: 02-01-06
```

Property pairs are used primarily in report generation. When defined, values such as Vessel or
Country are displayed on GPS and GPS Events reports.

The following pairs are used in the default GPS reports:

* vessel
* country
* contact
* frequency
* bandwidth
* collectedBy1
* collectedBy2
* collectedBy3
* collectedBy4
* satellite 

# Reporting

## From the Local Manager

GPS data is sorted into two categories; events and position information. Once the GPS device is
installed, GPS data is appended to all event logging.

When viewing event history, you will be able to see the exact location at which the event took
place.

To view event history, use the **show gps events** command.

```
[admin@UplogixLM (port1/1)]# show gps events
GMT Latitude Longitude Context Message
----- --------------- --------------- ------- --
18:37 30d 16' 13.854" N 97d 44' 28.716" W User djones logged in
18:37 30d 16' 13.854" N 97d 44' 28.716" W Power Cycled Port 1
18:38 30d 16' 13.848" N 97d 44' 28.716" W User Termed-in Port 2
18:38 30d 16' 13.848" N 97d 44' 28.716" W User djones logged out
```

In the above example, you can see that each event includes the latitude and longitude of the
LM at the time that the event was generated.

To view historical position information, use the show gps position command.

```
[admin@UplogixLM (port1/1)]# show gps position
EDT Latitude Longitude Satellites
-------- ----------------- ----------------- -----
17:56:51 30d 16' 13.854" N 97d 44' 28.710" W 9
17:57:21 30d 16' 13.854" N 97d 44' 28.710" W 10
17:57:51 30d 16' 13.854" N 97d 44' 28.710" W 10
17:58:21 30d 16' 13.854" N 97d 44' 28.710" W 10
17:58:51 30d 16' 13.854" N 97d 44' 28.710" W 10
17:59:21 30d 16' 13.854" N 97d 44' 28.710" W 10
17:59:51 30d 16' 13.854" N 97d 44' 28.716" W 10
18:00:21 30d 16' 13.854" N 97d 44' 28.710" W 10
```
This information is also archived and uploaded to an Uplogix Control Center, if configured.
 
## From the Control center

GPS data is available on the UCC in the form of reports. To access this information, select the
LM from the inventory list to bring up the LM Summary Page. Expand the port that contains
the GPS device and observe the GPS and GPS Events entries under Reports.

The GPS location report conforms to 47 C.F.R. Â§ 25.222 (c)(1) and is customizable through the
use of port properties.

# Exporting GPS Data via SNMP 

Stored GPS data can be accessed via SNMP if:

* SNMP is enabled on the LM
* The **_snmp_1.3.6.1.4.1.10243.10.1.5.5** property is set to **enabled**
* GPS data is being collected and stored in the database

## Enable SNMP

If SNMP has not already been enabled for your LM, use the **config system snmp** command to turn it on. The SNMP service has several options for security and access control. For this example, we will be using a basic security policy.

```
[admin@UplogixLM]# config system snmp
--- Existing  Values ---
SNMP is disabled.
Change these? (y/n) [n]: y
--- Enter New Values ---
Security Level (disabled,authPriv,noAuthNoPriv,authNoPriv) [disabled]: noAuthNoPriv
Port [161]: 
Username: admin
Do you want to commit these changes? (y/n): y
```

## Set System Property

Use the **config system properties** command to enable GPS via SNMP.

```
[admin@UplogixLM]# config system properties
[config properties]# _snmp_1.3.6.1.4.1.10243.10.1.5.5 enabled
[config properties]# exit
```

## (Optional) Install Uplogix MIB

Consult your SNMP agent's documentation for instructions on how to install a MIB file. If you are using the **snmpwalk** command in Linux, you can copy uplogix-mib.txt to ~/.snmp/mibs/.

The uplogix-mib.txt can be found the Uplogix Control Center under /home/emsadmin/.

## Use snmpwalk to view GPS data

The LM will only respond to SNMP Version 3 requests, though it responds with a Version 2 answer. Build your **snmpwalk** request similar to the one below. Replace the IP address as needed.

```
snmpwalk -v 3 -l noAuthNoPriv -u admin -m +UPLOGIX-SMI 172.30.5.30 1.3.6.1
```

The relevant output will start with UPLOGIX-SMI.

```
UPLOGIX-SMI::uplogixMostRecentGpsPort.0 = STRING: port1/1
UPLOGIX-SMI::uplogixMostRecentGpsPositionFixTime.0 = STRING: 2014-2-14,1:59:24.0,+0:0
UPLOGIX-SMI::uplogixMostRecentGpsLatitude.0 = STRING: 49.274167
UPLOGIX-SMI::uplogixMostRecentGpsLongitude.0 = STRING: -123.185333
UPLOGIX-SMI::uplogixMostRecentGpgll.0 = STRING: $GPGLL,4916.45,N,12311.12,W,015924.000,A*25
UPLOGIX-SMI::uplogixMostRecentGpgll.0 = No more variables left in this MIB View (It is past the end of the MIB tree)
```

If there is no data available to display, the values will be blank:

```
UPLOGIX-SMI::uplogixMostRecentGpsPort.0 = STRING: 
UPLOGIX-SMI::uplogixMostRecentGpsPositionFixTime.0 = STRING: 
UPLOGIX-SMI::uplogixMostRecentGpsLatitude.0 = STRING: 
UPLOGIX-SMI::uplogixMostRecentGpsLongitude.0 = STRING: 
UPLOGIX-SMI::uplogixMostRecentGpgll.0 = STRING: 
UPLOGIX-SMI::uplogixMostRecentGpgll.0 = No more variables left in this MIB View (It is past the end of the MIB tree)
```

If you did not install the uplogix-mib, the data will still be there, but the names won't be as descriptive. In this example, there is also no GPS data to display.

```
SNMPv2-SMI::enterprises.10243.10.1.5.5.1.1.0 = ""
SNMPv2-SMI::enterprises.10243.10.1.5.5.1.2.0 = ""
SNMPv2-SMI::enterprises.10243.10.1.5.5.1.3.0 = ""
SNMPv2-SMI::enterprises.10243.10.1.5.5.1.4.0 = ""
SNMPv2-SMI::enterprises.10243.10.1.5.5.2.1.0 = ""
SNMPv2-SMI::enterprises.10243.10.1.5.5.2.1.0 = No more variables left in this MIB View (It is past the end of the MIB tree)
```