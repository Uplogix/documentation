<!-- 5.4 -->

Configures the virtual ports on a Local Manager.  Virtual ports are connected via an intermediate console server over a network connection or utilizing a COM port redirector providing the same functionality the hardware versions.

Virtual ports are also used when communicating directly to a managed device on its management telnet port with reduced functionality. Ports may display UNAVAILABLE if the Local Manager cannot establish an RFC-2217 connection to the ip/port.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system slot <1 | 2 | 3 | 4 | modem | powercontrol>
```

# Usage 

Changing the slot settings may stop communication with a managed device.  Slot 4 is reserved for Virtual ports on Uplogix hardware Local Managers

```
[admin@UplogixLM]# config system slot 1
[config system slot 1]# 1 1.1.1.1 2001
Port 1 added.
[config system slot 1]# 2-15 1.1.1.2 2001
Port 2 added.
Port 3 added.
Port 4 added.
Port 5 added.
Port 6 added.
Port 7 added.
Port 8 added.
Port 9 added.
Port 10 added.
Port 11 added.
Port 12 added.
Port 13 added.
Port 14 added.
Port 15 added.
[config system slot 1]# exit
```
To remove a port use the [no] modifier before the port number 


```
[admin@UplogixLM]# config system slot 1
[config system slot 1]# no 1 1.1.1.1 2001
[config system slot 1]# exit
```

# In the Uplogix web interface 

**Inventory > Local Manager page > System > Virtual Slots** - specific to this system

# History 

4.4 - This command was introduced.

4.5 - Slot 4 option added for Hardware Local Managers

# Related commands 

- **show system slot**
