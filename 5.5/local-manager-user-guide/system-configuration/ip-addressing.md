<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary >Â Network > IP</div>

The Uplogix Local Manager is initially configured to use DHCP on IPv4 networks and autoconf on IPv6 networks.

# Viewing IPv4 Information

To view current IPv4 settings and other interface information, use the **show system ip** command.

```
[admin@UplogixLM]# show system ip
Use DHCP: Yes
Management IP: 10.200.2.98
Host Name: UplogixLM1
Subnet Mask: 255.255.255.0
Broadcast Address: 10.200.2.255
Default Route: 10.200.2.1
Speed/duplex: auto
DNS Server: 
MAC Address: 00:0F:2C:00:15:23
Bonding Link: yes
Front Ethernet Link: yes (bonded primary)
Aux1 Ethernet Link: yes (outband)
Aux2 Ethernet Link: no (bonded)
```

# Modifying IPv4 Configuration

To change the IP settings, use the **config system ip** command.

```
[admin@UplogixLM]# config system ip
--- Existing Values ---
Use DHCP: No
Management IP: 172.30.151.100
Host Name: UplogixLM1
Subnet Mask: 255.255.255.0
Broadcast Address: 172.30.151.255
Default Route: 172.30.151.254
Speed/duplex: auto:100full
DNS Server: 
MAC Address: 00:0F:2C:00:15:23
Bonding Link: yes
Front Ethernet Link: yes (bonded primary)
Aux1 Ethernet Link: yes (bonded)
Aux2 Ethernet Link: no (bonded)
Change these? (y/n) [n]:
```

Configurable settings include DHCP, Management IP, Hostname, Subnet Mask, Default Route, Speed/Duplex, and DNS Server. All other fields are populated automatically.

**Zero Touch DNS:** The Local Manager can automatically configure DNS settings if 1) DHCP is enabled and 2) the DHCP server has been configured to return one or multiple DNS servers.

```
Use DNS (y/n) [y]: 
Automatically configure DNS (y/n) [y]:
```

# IPv6 Configuration

<div class='ucc' />Inventory > Local Manager Summary >Â Network IPv6</div>

To view current IPv6 settings, use the **show system ipv6** command.

```
[admin@UplogixLM]# show system ipv6
Mode: autoconf
Management IP: 2001:470:b851:301:20f:2cff:fe00:ccec/64
Default Route:
```

To change IPv6 settings, use the **config system ipv6** command.

```
[admin@UplogixLM]# config system ipv6
--- Existing  Values ---
Mode: autoconf
Management IP: 2001:470:b851:500:20f:2cff:fe00:cbc2/64
Default Route:

Change these? (y/n) [n]: y
--- Enter New Values ---
Mode [autoconf]: static
Management IPv6 [2001:470:b851:500:20f:2cff:fe00:cbc2/64]: 2001:470:b861:20:0:0:0:51/64
Default Route: 2001:470:b861:20::1
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): y
```

> Not all product features support the use of IPv6.