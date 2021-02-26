<!-- 5.4 -->

This command allows you to retrieve diagnostic information from network devices when necessary. The information gathered depends on the device. You can view the information using the show tech command. 

# Command availability

CLI resource: port, modem

Device makes: Alcatel, Cisco, Netscreen

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
pull tech
```

# Usage 

```
[admin@UplogixLM (port1/1)]# pull tech
Pull tech completed and saved as current.
```
```
[admin@UplogixLM (modem)]# pull tech
Checking Product Code
Checking Firmware
Checking Line Voltage
Checking Modem Register Values
Checking Previous Call Data
Checking Dial Tone
Pull tech completed and saved as current.
```

# In the Uplogix web interface

Pull operations are automatically scheduled by Uplogix Control Center.

# History 
--
#Related commands 

- **show tech**
