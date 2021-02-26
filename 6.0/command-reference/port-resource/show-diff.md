<!-- 5.4 -->

Displays differences between versions of similar configuration elements.

# Command availability

CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show diff <running-config | startup-config | post> <â€œfile versionâ€> <â€œfile versionâ€>
```

# Usage 
Additions are prefixed with **+**; deletions are prefixed with **-**.

```
[admin@xyzcoAus01 (port1/1)]# show diff running-config
previous Fri Oct 07 02:07:34 UTC 2005
current Sun Oct 09 19:09:11 UTC 2005
interface FastEthernet3/13
+ switchport access vlan 75
- switchport access vlan 315
```

# History 

2.0 - This command was introduced.

# Related commands 

--
