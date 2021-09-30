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
Host Name: xyzcoAus01
Subnet Mask: 255.255.254.0
Broadcast Address: 198.51.238.255
Default Route: 172.30.5.254
Speed/duplex: auto:100full
MAC Address: 00:0F:2C:00:CA:94
Use DNS: no
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: yes (bonded)
```

# In the Uplogix web interface

**Inventory > Local Manager page > Network > IP** - specific to this system

# History 
3.4 - This command was introduced to replace show Local Manager ip.

# Related commands 

- **config system ip**
