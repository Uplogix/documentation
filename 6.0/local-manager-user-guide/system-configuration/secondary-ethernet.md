<div class='ucc' />Inventory > Local Manager Summary >Â Network > Secondary Ethernet</div>

The Local Manager's secondary Ethernet port can operate in one of four modes:

* **Bonded** &mdash; Use this default mode to join the Secondary Ethernet interface with the front management interface to form a single logical network interface. This mode is most useful for failover scenarios.
* **Capture** &mdash; Use this mode to enable the capture of network traffic for troubleshooting purposes.
* **DHCPServer** &mdash; Use this mode to enable WAN Traffic Failover and out-of-band connection sharing.  This enables a local router to route traffic through the Local Manager and over the cellular out-of-band connection when the WAN link fails - see the WAN Traffic Failover feature for more details.
* **Outband** &mdash; Use this mode to configure a secondary management network to be used as an out-of-band channel.

# Physical Connection

Connect the secondary Ethernet port on your Local Manager to your alternate/out-of-band network connection using this port. The following list identifies the secondary Ethernet port for each Local Manager platform:

### Uplogix LM80/83X
Use the GE-1 port located below Management Ethernet port GE-0.

### Uplogix 500/5000
Use the GE-1 port located below Management Ethernet port GE-0.

### Uplogix 3200

Use the AUX port located on the back of the device beneath the power controller port.

### Uplogix 430

Use the AUX port located to the left of the power controller port.

### Uplogix 400

Use the AUX 1 port located on the back of the device.

# Bonded Mode

This mode is enabled by default, even if no physical connection is present. Both Ethernet interfaces are combined into a single logical bond0 Ethernet management interface. If a switch port, cable, or interface fails on the primary Ethernet port connection, the system will automatically fail over to the secondary Ethernet connection.

## Usage Notes

* Both network interfaces need to be connected to the same VLAN.
* The bond0 interface will use the MAC address of the primary interface. The show system secondary command will not display a MAC address for the secondary Ethernet interface while in this mode.

# Capture Mode

This mode allows the capture and review of network traffic via the secondary Ethernet interface. A switch can be configured to span/mirror traffic to a port that is connected to the secondary Ethernet port of the Local Manager, where the Local Manager can then capture, filter, display and export traffic captures.

## Usage Notes

* The directly connected switch must be configured to send traffic to the Local Manager's secondary Ethernet port.
* The maximum size of the capture file is 5MB. Traffic capture will automatically stop when this limit is reached.

## System Configuration

To configure capture mode, run **config system secondary** from the system resource. When asked for type, specify 'capture' and options will become available for speed/duplex.

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: capture
speed/duplex [auto]:
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): y

```

## Capturing Packets (Basic)

To begin capturing packets, use the **capture** command from the system resource. Capture will continue until you press x, CTRL-C, or the 5MB capture limit is reached.

```
[admin@UplogixLM]# capture
Press 'x' or Ctrl+C to stop capturing packets.
4864 bytes
Capture stopped.
```

## Capturing Packets (Advanced)

A variety of options for the **capture** command are available to filter captured packets.

| Option | Syntax |
| :- | :- |
| IP Address |	capture host 192.168.1.100
| Network |	capture net 192.168.1.0/24
| Port |	capture port 80
| IP Address and Port | capture host 192.168.1.100 and port 80
| Source	| capture src 192.168.1.1
| Destination | capture destination 192.168.1.253
| Frame Size | capture greater 512, capture less 128
| Bytes Per Frame | capture -size 1514

## Viewing Captured Packets

To view captured packets, use the show capture command from the system resource.

```
[admin@UplogixLM]# show capture
18:53:25.281292 CDPv2, ttl: 180s, Device-ID '333A'[|cdp] 
18:53:25.284526 CDPv2, ttl: 180s, Device-ID '333A'[|cdp] 
18:53:25.287029 CDPv2, ttl: 180s, Device-ID '333A'[|cdp] 
18:53:25.926118 802.1d config TOP_CHANGE 8000.00:d0:ba:bf:62:cd.8022 root 2000.00:d0:01:c1:c4:34 pathcost 23 age 3 max 20 hello 2 
fdelay 15 
18:53:26.315752 IP6 :: > ff02::16: HBH ICMP6, multicast listener report v2, 1 group record(s), length 28 
18:53:26.391749 IP6 :: > ff02::1:ff00:1524: ICMP6, neighbor solicitation, who has fe80::20f:2cff:fe00:1524, length 24 
18:53:26.942055 802.1d config TOP_CHANGE 8000.00:d0:ba:bf:62:cd.8022 root 2000.00:d0:01:c1:c4:34 pathcost 23 age 2 max 20 hello 2 
fdelay 15 
18:53:27.391840 IP6 fe80::20f:2cff:fe00:1524 > ff02::2: ICMP6, router solicitation, length 16 
18:53:28.358245 802.1d config TOP_CHANGE 8000.00:d0:ba:bf:62:cd.8022 root 2000.00:d0:01:c1:c4:34 pathcost 23 age 2 max 20 hello 2 
fdelay 15
```

To export the capture file in pcap format, use the **show capture -pcap** command and pipe it to SCP, FTP, or E-mail.

```
[admin@UplogixLM]# show capture -pcap | scp uplogix@203.0.113.5:u5000.cap1
uplogix@203.0.113.5's password:*******
..
File successfully sent to 203.0.113.5.
copy succeeded
```

To export via E-mail, use the following syntax:

```
[admin@UplogixLM]# show capture -pcap | mailto support@uplogix.com:u5000.cap1
..
File successfully sent to uplogix.com.
copy succeeded
```

In the above example, the capture file will be attached to the email with the filename u5000.cap1. You can then view this file in any third party application capable of reading pcap files like Wireshark, etc.

To export the capture file in plain text with SCP, FTP, or E-mail, simply omit the - pcap option.

# DHCPServer Mode

This mode allows the secondary Ethernet interface to operate as a WAN Traffic Failover interface for a local router, where traffic received from the router will be forwarded over the out-of-band cellular network connection when the primary Network/WAN is down.  

## Usage Notes

* The routed interface that is connected to the secondary Ethernet port should be configured to use DHCP in order to get an IP address from the Local Manager secondary Ethernet port.
* The Local Manager PPP settings must be configured to *Enable Out-of-Band Sharing (y/n)* before the secondary Ethernet interface can be configured to *Forward traffic over Out-of-Band Connection (y/n)*.  To configure PPP settings, run **config ppp** from the modem resource.
* When configuring this mode, leave the *DHCP MAC Address Filter* field blank if you want the Local Manager to offer an IP address to whatever device makes a request (safe when directly connecting the router routed interface to the Local Manager's secondary Ethernet interface).  If you want the Local Manager to only respond to DHCP requests from a specific device or type of device, enter a full MAC address or MAC address prefix for the device that will be routing traffic to the Local Manager WAN Traffic Failover interface - this prevents the Local Manager from becoming a generic DHCP server to other devices for the case where another device might attempt to DHCP an IP address..


## System Configuration

To configure DHCPServer mode, run **config system secondary** from the system resource. When asked for type, specify dhcpserver and options will become available for DHCP MAC filter and speed/duplex.

The following example uses DHCPserver.

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: dhcpserver
DHCP MAC Address Filter: 
speed/duplex [auto]: 
Forward traffic over Out-of-Band Connection (y/n) [n]: y
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): y
```

## Viewing Secondary Ethernet DHCPServer Configuration

To view the DHCPServer settings on the secondary Ethernet interface, use the **show system secondary** command from the system resource. Note that the device IP shown below is the IP address given to the failover interface on the connected router.

```
[admin@UplogixLM]# show system secondary
Type: dhcpserver
Device IP: 169.254.100.254
Port IP: 169.254.100.253
Subnet: 255.255.255.252
Speed/duplex: auto (no link)
MAC Address: 00:0F:2C:00:CF:07
Forward traffic over Out-of-Band Connection: yes
```

# Outband Mode

This mode allows the secondary Ethernet interface to be configured as an out-of-band channel for use during primary network outages.

To configure outband mode, run **config system secondary** from the system resource. When asked for type, specify 'outband' and options will become available for DHCP, speed/duplex, and DNS. If not using DHCP, the device will prompt for IP address, subnet mask, and default route.

The following example uses DHCP.

```
[admin@uplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: outband
Use DHCP (y/n) [n]: y
speed/duplex [auto]:
Use DNS (y/n/auto) [auto]:
Enable Out-of-Band Sharing (y/n) [n]:
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): y
```



## Usage Notes

* The secondary IP subnet must not conflict with the primary and dedicated IP subnets of the Local Manager.
* The secondary Ethernet interface is disabled during in-band operation. The interface will not respond to IP traffic until the out-of-band connection is enabled.
* If you want the Local Manager to establish a VPN over this secondary Ethernet connection, be sure to configure the VPN settings. Use the config vpn command from the modem resource to configure VPN settings.
* Dial-in access via the modem is available through the config answer command. PPP dial-up via the modem is disabled in this mode.

Outband mode is further discussed in [Secondary Ethernet Access](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/configuring-secondary-ethernet).