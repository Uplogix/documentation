<!-- 5.4 -->

Displays the Uplogix Local Manager's current management address, Ethernet speed, and hostname.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system ip
```

# Usage 

```
[admin@UplogixLM]# show system ip
Use DHCP: Yes
Management IP: 198.51.238.102
Host Name: UplogixLM
Subnet Mask: 255.255.254.0
Broadcast Address: 172.30.5.255
Default Route: 172.30.5.254
Speed/duplex: auto
MAC Address: 00:0F:2C:01:81:64
Use DNS: auto
DNS Server 1: 172.30.4.253
DNS Server 2: 172.30.111.253
Domain Search: uplogix.local
Bonding Link: yes
[E1] Primary Ethernet Link: yes (bonded active)
[E2] Auxiliary Ethernet Link: no (capture)
[E3] Internal SFP Ethernet Link: no (bonded)
```

# In the Uplogix web interface

**Inventory > Local Manager page > Network > IP** - specific to this system

# History 
3.4 - This command was introduced to replace show Local Manager ip.

# Related commands 

- **config system ip**
