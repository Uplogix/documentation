Configures the Local Manager's network addressing.

A Local Manager is initially configured to use DHCP. You can use the **show system ip** command to display current management Ethernet network settings. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All
# Syntax

```
config system ip
```

# Usage

```
[admin@UplogixLM]# config system ip
--- Existing Values --- 
Use DHCP: Yes 
Management IP: 0.0.0.0
Host Name: UplogixLM
Subnet Mask: 255.255.255.0 
Broadcast Address: 0.0.0.255 
Default Route: 0.0.0.0 
Speed/duplex: auto: 1000full
MAC Address: 00:0F:2C:00:CC:C6 
Bonding Link: yes
Primary Ethernet Link: yes (bonded)
Auxiliary Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values --- 
Use DHCP: (y/n) [y]: n
Management IP: [0.0.0.0]: 198.51.100.4
Host Name: [UplogixLM]: 
Subnet Mask: [255.255.255.0]: 
Default Route: [0.0.0.0]: 198.51.100.254
speed/duplex: [auto:1000full]: 
Use DNS (y/n) [y]: 
Automatically configure DNS (y/n) [y]: n
DNS Server IP 1: 172.30.4.252
DNS Server IP 2:  
Domain Search: 
Warning: Remote connections may be lost if you commit changes. 
Do you want to commit these changes? (y/n): y
```

# In the Uplogix web interface

**Inventory > Local Manager page > Network > IP** - specific to this system

# Related commands 

- **show system ip**