<!-- 5.4 -->

Displays collected running configuration from a device.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, Comtech EF Data, Foundry, Garmin, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sea Tel, Sun, Tasman, TippingPoint

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show running-config [candidate | current | previous | <user ver> | archive #]

```
# Usage 

```
[admin@UplogixLM (port1/1)]# show running-config 
!
version 12.0
no service pad
service Timestamps debug uptime
service Timestamps log uptime
no service password-encryption
!
hostname DMZ-2948
!
no logging console
!
!
interface FastEthernet1
 no ip address
 no ip directed-broadcast
 no ip mroute-cache
 bridge-group 1
!
interface FastEthernet2
 no ip address
 no ip directed-broadcast
 no ip mroute-cache
 bridge-group 1
!
interface FastEthernet3
 no ip address
 no ip directed-broadcast
 no ip mroute-cache
< example text removed >
```

# In the Uplogix web interface

Inventory > Local Manager page > port detail > Files - specific to this device

# History 

1.4 - Archive added. 

# Related commands 

- **pull running-config**
- **show startup-config**
