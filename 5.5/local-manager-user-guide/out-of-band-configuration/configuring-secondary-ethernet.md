<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary >Â Network > Secondary Ethernet</div>

In addition to modems, the Local Manager can use its secondary Ethernet port as an out of band channel.

# Usage Notes

* The secondary network must not conflict with the applianceâ€™s primary and dedicated networks. 
* The secondary Ethernet interface is turned off during in-band operation. The interface will not respond to pings until the out of band connection is enabled.
* Dial-in access via the modem is available through the **config answer** command. Dial-up PPP via the modem is disabled in this mode.

# Configure Outband Mode

To configure outband mode, run **config system secondary** from the system resource. When asked for type, use *outband*. Once outband is specified, options will become available for DHCP, speed/duplex, and DNS. If you are not using DHCP, the system will prompt for IP address, subnet mask, and default route.

## Using DHCP

The following example uses DHCP, auto-negotiated speed/duplex, automatic DNS, and no out-of-band sharing.

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: yes (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: outband
Use DHCP (y/n) [n]: y
speed/duplex [auto]: 
Use DNS (y/n) [y]: y
Automatically configure DNS (y/n) [y]: y
Enable Out-of-Band Sharing (y/n) [n]: 
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): 
```

## Using Static IP Addresses

To specify the out-of-band IP address, run **config system secondary** again and set DHCP to n

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: yes (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: outband
Use DHCP (y/n) [n]: n
Management IP: 192.168.1.1
Default Route: 192.168.1.254
Subnet Mask: 255.255.255.0
speed/duplex [auto]: 
Use DNS (y/n) [y]: 
Automatically configure DNS (y/n) [y]: n
DNS Server IP 1: 192.168.1.254
DNS Server IP 2: 192.168.1.253
Domain Search: uplogix.local
Enable Out-of-Band Sharing (y/n) [n]: n
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): 
```

## Using Automatically Configured DNS

If you are using DHCP to assign an IP address to the Local Manager, you can optionally enable automatic configuration of DNS if the DHCP server is configured to return the nameserver's IP address(es).

```
Use DNS (y/n) [y]: 
Automatically configure DNS (y/n) [y]: y
```

## Enabling Out-of-band Sharing

This feature is used with WAN Traffic Failover. Please contact Uplogix Support for more information.

# Enabling Outband Manually

To bring up the out-of-band interface, use the **outband on** command from the modem resource.

```
[admin@UplogixLM (modem)]# outband on
Secondary Ethernet Adapter is down.
Secondary network Local Address is 172.30.52.111
Out of Band is turned on.
```

The message *Secondary Ethernet Adapter is down* refers to the adapterâ€™s status prior to running outband on. If PPP is already up, the following message will be displayed.

```
[admin@UplogixLM (modem)]# outband on
Secondary Ethernet Adapter is up.
```

To turn off the outband connection, use the **outband off** command.

```
[admin@UplogixLM (modem)]# outband off
Out of Band is turned off
```

# Enabling Outband Automatically

The outband connection can be activated from built-in features like Pulse and through the rules engine. Note that while some commands continue to reference PPP, no PPP connection will be established.

```
[admin@UplogixLM]# config system pulse
--- Existing  Values ---
Use Pulse: false
Pulse Server IP 1: 127.0.0.1
Pulse Server Port 1: 7
Enable Out-of-Band on Pulse Failure: no
Change these? (y/n) [n]: y
--- Enter New Values ---
Use Pulse (y/n) [n]: y
Pulse IP 1 [127.0.0.1]: 10.10.10.1
Pulse Port 1 [7]: 
Pulse IP 2 [127.0.0.1]: 
Pulse Port 2 [7]: 
Pulse IP 3 [127.0.0.1]: 
Pulse Port 3 [7]: 
Enable Out-of-Band on Pulse Failure (y/n) [n]: y
Remain Out-of-Band after Pulse Success (y/n) [n]: n
Maximum Time Out-of-Band (0 means unlimited) [0]: 
Do you want to commit these changes? (y/n): 
```

If Pulse fails, the system will automatically enable the outband connection.

```
[admin@UplogixLM]# show alarms
UTC   Elapsed Device Interface Message
----- ------- ------ --------- --------------------------------------
14:09 0:40                     Failed to connect to pulse server.

[admin@UplogixLM]# show event
UTC   Context            Message
----- ------------------ ----------------------------------------------------
12:56                    PPP is up. (192.168.1.1)
```

You can also use a rule to bring up the Secondary Ethernet connection. The following is a simplified example that turns outband on upon scheduling. Note that pppOn is specified as the action, but will have the same effect as **outband on**.

```
[admin@UplogixLM]# config rule pppAlwaysOn
[config rule pppAlwaysOn]# action pppOn
[config rule pppAlwaysOn]# action alarm -a "Enabling Secondary Ethernet OOB"
[config rule pppAlwaysOn]# conditions
[config rule pppAlwaysOn conditions]# true
[config rule pppAlwaysOn conditions]# exit
[config rule pppAlwaysOn]# exit

[admin@UplogixLM]# config monitor system pppAlwaysOn
Validate scheduled monitor(system)? (This will execute the job now.) (y/n): y
Job was scheduled 4: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor system pppAlwaysOn

[admin@UplogixLM]# show alarms
UTC   Elapsed Device Interface Message
----- ------- ------ --------- --------------------------------------
14:38 0:24                     Enabling Secondary Ethernet OOB
Viewing Secondary Ethernet Status
```

You can use the **show status** command from the modem resource to view out of band information.

```
[admin@UplogixLM (modem)]# show status
Outband: Secondary Ethernet
Inactive

[admin@UplogixLM (modem)]# show status
Outband: Secondary Ethernet
Active: address 172.30.52.111, duration 10 minutes
```

# Disabling Outband Mode

To disable outband mode on Secondary Ethernet, run **config system secondary** from the system resource. When asked for type, use *bonded*.

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: outband
Use DHCP: No
Management IP: 192.168.1.1
Default Route: 192.168.1.254
Subnet Mask: 255.255.255.0
Speed/duplex: auto (no link)
MAC Address: 90:0F:2D:00:CB:C3
Use DNS: no
Enable Out-of-Band Sharing: no
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [outband]: bonded
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): y

[admin@UplogixLM]# 
```
