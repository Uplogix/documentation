# Overview

There are a variety of cases where typical console device management may be impractical or impossible. For these deployments, the Local Manager can be configured to use virtual device management ports. These virtual ports mimic the functionality of the physical serial interfaces on the front of your Local Manager. Some cases where virtual ports are applicable include:

* Manage devices where the distance between the Local Manager and the managed device is too far for a RS-232 serial connection or where there is an inability to run additional cables.
* Manage devices already connected to a console server.
* Manage devices whose serial ports are being used for other purposes.
* Manage devices with IP connectivity but no serial connectivity.
* Manage devices using an Local Manager virtual machine (VM) running on a VMware ESXi server.

This feature requires the purchase of a virtual port license for each virtual port from Uplogix. [Licenses are installed on the Control Center](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/licenses). All virtual ports are limited to virtual slot 4 on Uplogix hardware platforms. The maximum number of allowable virtual ports varies on a platform basis as follows:

* **Uplogix 500** - 16 virtual ports supported
* **Uplogix 5000** - 16 virtual ports supported

To assure adequate performance on richly configured systems, Uplogix recommends that the sum of configured physical ports and virtual ports not exceed the total number of physical ports supported by the Uplogix platform. It is possible to exceed the recommended maximum port count and not experience degradation in performance â€“ performance will vary based on the amount of monitoring, automation and SLV tests that are configured, and based on the frequency of the monitors and the Local Managerâ€™s communication with the Control Center.

While all advanced drivers are configurable on virtual ports that terminate at a console server, Uplogix officially supports only the native, enhanced native, and Cisco IOS device drivers for virtual ports that terminate on the managed device (i.e., VTY/IP connection where no console server is involved).

Virtual ports that terminate on the managed device (i.e., VTY/IP connection where no console server is involved) do not support all of the functionality supported for managed devices that are directly or indirectly connected to the local manager via a serial console port connection. The following driver functionality is not available in this case:

* LAN independence
* Bare metal restore
* ROMmon recovery
* Password/Configuration recovery where boot loader configuration is required
* Power On Self Test (POST) data collection
* Automatic Rollback
* xmodem and ymodem file transfers	

The following privileges are required to configure virtual ports:

* **config system slot** â€“ Configure a virtual slot and virtual ports.
* **show system slot** â€“ View virtual slot/port configuration.
* **config system clear slot** â€“ Clear virtual slot configuration.
* **config system clear port** â€“ Clear port/virtual port data from the database.
 
# Configure a virtual port

To use virtual ports, you must first create a virtual slot. The slot number will depend on your hardware platform.

* Uplogix LM80/LM83X: slot 5
* Uplogix 500 / 5000: slot 4

Use the **config system slot {slot_number}** command to enter the virtual slot configuration editor. 

```
[admin@UplogixLM]# config system slot 5
```

Once in the editor, use the **?** command to view a list of possible configuration options.

```
[config system slot 5]# ?
Allowable arguments are:
show
[no] port <number|range> <IP> <TCP port> <ssh|ssh-vty|telnet> [-noroute]
config port <number> (to configure SSH credentials)
or 'exit' to quit config mode
? (to display help)

Maximum virtual ports supported: 16
```

Specify **-noroute** if the virtual port connection should route over an out-of-band connection when it is available.

<div class='warning' /> The **-noroute** option may also be necessary if the target device is on the same connected network as the Local Manager. If pings to a device succeed at first but fail after adding the port *and* a terminal session fails, try modifying the port configuration to include **-noroute**.</div>

```
Examples:
========
Adding virtual ports:
port 1 192.168.100.20 22 ssh
port 2 192.168.100.21 22 ssh-vty
port 3-8 172.30.100.2 6003 telnet
* Additional prompts will appear if the port type is SSH.
```

> The **ssh** connection type will prompt for a username and password to serve as the configured authentication. When a user runs **terminal**, the Local Manager will automatically authenticate using the stored settings. To force the user to authenticate with the virtual port each time they run **terminal**, use **ssh-vty** instead.

## SSH Example

In this example, a virtual port is added for a Linux server at 198.51.100.100 on port 22. A functional ID (sysop) is used for automatic authentication of **terminal** sessions.

```
[admin@UplogixLM]# config system slot 5
[config system slot 5]# port 1 198.51.100.100 22 ssh
Port 1 added.
Adding route 198.51.100.100
Username: sysop
The authenticity of host '198.51.100.100' cannot be established.
Fingerprint: ac:a2:5e:67:e0:40:fe:77:b7:db:b7:26:2d:08:6f:28 (2048)
    SHA-256: c4I+WipGo4JYpMBg8GPwpczNy+Py0fpU20ocC0aLlX8=

Are you sure you want to continue connecting (y/n): y
Public key authentication failed for: sysop
Password: *******
Confirm Password: *******
Successfully connected using password.
Type 'exit' to quit the configuration editor or '?' for more options.
Removing route 198.51.100.100
[config system slot 5]# exit
```

## SSH-VTY Example

In this example, a virtual port is added for a Linux server at 198.51.100.101 on port 22. No authentication information is specified, forcing users to authenticate with the managed device after running the **terminal** command.

```
[config system slot 5]# port 2 198.51.100.101 22 ssh-vty 
Port 2 added.
Adding route 198.51.100.101
Test username (optional): 
The authenticity of host '198.51.100.101' cannot be established.
Fingerprint: 1b:58:2a:1b:83:49:90:19:0e:b7:c7:0b:b6:89:0b:9c (2048)
    SHA-256: 9d28.cb05.ed2e.c1c3.d0ec.6df7.ba7e.310b
             cc94.5978.712d.7624.d2ce.e744.a713.4306

Accept host key (y/n): y
Type 'exit' to quit the configuration editor or '?' for more options.
Removing route 198.51.100.101
```

# Removing virtual ports

```
no port 1 
no port 3-8
```

In some cases, re-configuration of a removed port may require exit and re-entry of virtual port slot configuration.

# Editing SSH virtual port credentials

```
config port 2 
```

* You must remove and recreate the SSH virtual port if you want to clear any parameter

* You do not need to enter a password if you are using SSH public key authentication to the remote device. When using public key authentication, be sure to place the Local Manager public key in the appropriate location on the managed device prior to configuring the virtual port here. Use the **show system crypto certificate virtual** command to display the Local Manager public key.

```
[config system slot 5]#
```
 
**Command definitions:**

 * **show** Display the current virtual slot/port configuration.
 * **[no] port [number | range] [IP] [TCP port] [ssh | telnet] [-noroute]** Define virtual ports. Use the SSH option to use secure virtual ports. Only add the â€“noroute parameter if the virtual port traffic should be routed over the Local Managerâ€™s out-of-band network connection during an in-band network connectivity failure (not typically used, as most use cases call for always routing virtual port traffic over the LAN/in-band network connection on the Local Manager). Use the no option to remove virtual port(s) from the virtual slot.
 * **config port [number]** Configure SSH authentication credentials for a secure virtual port.
 * **Exit** Exit the configuration editor.

Once the virtual slot has been configured on the Local Manager, create virtual ports for managed devices. Below are a few examples of how to create and map virtual ports to managed devices:

Map virtual port 1 to TCP port 6001 of a console server with an IP address of 192.0.2.101:

```
port 1 192.0.2.101 6001 telnet
```

Map virtual port 2 to SSH TCP port 22 on a managed device with IP address 192.0.2.100:

```
port 2 192.0.2.100 22 ssh
```

Map virtual ports 3 and 4 to TCP ports 6002 and 6003 of a console server with IP address 192.0.2.101 using the **range** command (assumes contiguous TCP ports).

```
port 3-4 192.0.2.101 6002 telnet
```

To view the virtual slot configuration editor, use the **show system slot {slot_number}** command. Slot 4 is the only virtual slot allowed for Local Manager hardware.

```
[admin@UplogixLM]# show system slot 5
1 192.0.2.101 6001 Telnet
2 192.0.2.100 22 SSH
3 192.0.2.101 6002 Telnet
4 192.0.2.101 6003 Telnet
```

# Delete a virtual port

Use the **config system slot [slot_number]** command to enter the virtual slot configuration editor and and the **no port [port_number]** command to delete a particular virtual port.

This example deletes virtual port 2 from virtual slot 5:

```
[admin@UplogixLM]# config system slot 5
[config system slot 5]# show
1 192.0.2.101 6001 Telnet
2 192.0.2.100 22 SSH
3 192.0.2.101 6002 Telnet
4 192.0.2.101 6003 Telnet
[config system slot 5]# no port 2
[config system slot 5]# show
1 192.0.2.101 6001 Telnet
3 192.0.2.101 6002 Telnet
4 192.0.2.101 6003 Telnet
[config system slot 5]# exit
```

Once a virtual port is deleted, it is necessary to clear the database and dashboard of information associated with the deleted virtual port by using the **config system clear port {port_number}** command.