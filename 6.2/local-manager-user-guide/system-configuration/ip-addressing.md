<div class='ucc' />Inventory > Local Manager Summary > Network > IP</div>

The Uplogix Local Manager is initially configured to use DHCP on IPv4 networks and autoconf on IPv6 networks.

# Viewing IPv4 Information

To view current IPv4 settings and other interface information, use the **show system ip** command.

```
[admin@UplogixLM]# show system ip
Use DHCP: Yes
Management IP: 10.10.10.59
Host Name: UplogixLM
Subnet Mask: 255.255.254.0
Broadcast Address: 10.10.10.255
Default Route: 10.10.10.254
Speed/duplex: auto
MAC Address: 00:0F:2C:01:81:64
Use DNS: auto
DNS Server 1: 10.10.11.253
Bonding Link: yes
[E1] Primary Ethernet Link: yes (bonded active)
[E2] Auxiliary Ethernet Link: no (bonded)
[E3] Internal SFP Ethernet Link: no (bonded)
```

Previous Local Manager hardware platforms have a different naming scheme for Ethernet and SFP interfaces.

```
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: no (bonded)
```

# Modifying IPv4 Configuration

To change the IP settings, use the **config system ip** command.

```
[admin@UplogixLM]# config system ip
--- Existing  Values ---
Use DHCP: Yes
Management IP: 10.10.10.59
Host Name: A700000115
Subnet Mask: 255.255.254.0
Broadcast Address: 10.10.10.255
Default Route: 10.10.10.254
Speed/duplex: auto
MAC Address: 00:0F:2C:01:81:64
Use DNS: auto
DNS Server 1: 10.10.11.253
Domain Search: uplogix.local
Bonding Link: yes
[E1] Primary Ethernet Link: yes (bonded active)
[E2] Auxiliary Ethernet Link: no (bonded)
[E3] Internal SFP Ethernet Link: no (bonded)
Change these? (y/n) [n]: 
```

Configurable settings include DHCP, Management IP, Hostname, Subnet Mask, Default Route, Speed/Duplex, and DNS Server. All other fields are populated automatically.

**Zero Touch DNS:** The Local Manager can automatically configure DNS settings if 1) DHCP is enabled and 2) the DHCP server has been configured to return one or multiple DNS servers.

```
Use DNS (y/n/auto) [y]: auto
```

# IPv6 Configuration

<div class='ucc' />Inventory > Local Manager Summary > Network IPv6</div>

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