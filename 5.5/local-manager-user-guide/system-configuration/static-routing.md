<!-- 5.4 -->

# Configure a Static Route

For the case where a trunk is used to connect the Uplogix Local Manager to the network, the main management interface uses the trunk native VLAN (usually VLAN=1, unless otherwise specified in the switch port configuration), which is configured using the **config system ip** command. Use the **config system route** command to enter the route editor.

```
[admin@UplogixLM]# config system route
Warning: Remote connections may be lost if you commit changes.
[config route]#
```

Once in the editor, you can use the **?** command to view a list of possible configuration options.

```
[config route]# ?
Allowable arguments are:
show
[no] route
or 'exit' to quit config mode
```

Use the **route** subcommand to set an IPv4/IPv6 static route on the management interface. The **no** prefix will remove the static route.

For example, to route all outgoing traffic headed to the 192.168.1.0/24 network over the in-band management Ethernet interface, use **route 192.168.1.0/24**. To route all outgoing traffic headed for 2001&#58;200::0/32, use **route 2001&#58;200::0/32**.

Connectivity to the Uplogix LM will be temporarily lost while the route(s) are applied to the management interface.

IPv6 static routes can only be added to the management interface for the case where a static IPv6 address was assigned to the management interface using the config system ipv6 command (i.e. static IPv6 routes are not allowed if IPv6 auto configuration is enabled for the Local Manager).

# Display System Routes

Use the **show system route** command to view the Local Manager routing table, which includes user defined static routes on the management interface and subinterfaces. 

```
[admin@UplogixLM]# show system route
Destination Gateway Interface
Default 172.30.50.254 Management
10.0.1.0/24 172.30.51.254 voice
172.30.50.0/24 Management
172.30.51.0/24 voice
172.30.161.1/32 172.30.50.254 Management
192.168.1.0/24 172.30.50.254 Management
Default fe80::20a:41ff:fe7c:8d20 Management
Default 2001:100:b951:600:1222:ab71:fe01:2386 voice
2001:100::/32 2001:100:b951:600:1222:ab71:fe01:2386 voice
2001:100:b951:600::/64 voice
2001:470:b851:10::/64 Management
```