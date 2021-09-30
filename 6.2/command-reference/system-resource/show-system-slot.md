<!-- 5.4 -->

Displays the virtual ports on a Local Manager.  Virtual ports that are connected via an intermediate console server over a network connection or utilizing a COM port re-director provide the same functionality as the hardware versions.

Virtual ports are also used when communicating directly to a managed device on its management telnet port with reduced functionality. Ports may display UNAVAILABLE if the Local Manager cannot establish an RFC-2217 connection to the ip/port.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system slot <1 | 2 | 3 | 4 |modem | powercontrol>
```

# Usage 

```
[admin@UplogixLM]# show system slot 1
```

# In the Uplogix web interface 

**Inventory > Local Manager page > System > Virtual Slots** - specific to this system

# History 

4.4 - This command was introduced.

4.5 - Slot 4 option added for hardware Local Managers

# Related commands 

- **config system slot**
