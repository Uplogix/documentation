<!-- 5.4 -->

Displays credentials used to communicate with a device connected to the Uplogix Local Manager. Use the **show system authentication** command to display authentication information for the system itself.

# Command availability

CLI resource: port, powercontrol

Device makes: All

Uplogix system: All

LMS offerings: All

# Syntax 

```
show authentication
```

# Usage 

Passwords are always masked when displayed.

```
[admin@UplogixLM (port1/1)]# show authentication
console user: tasman	
console password: ********
enable user:
enable password: ********
```
# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all devices that match the selected filter

**Inventory > Local Manager page > port detail > schedule button** - specific to this device

# History 
--

# Related commands 
- **config authentication**
- **config system authentication**
- **show system authentication**
