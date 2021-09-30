<!-- 5.4 -->

Interactive command to specify VPN for the Uplogix Local Manager after outband connectivity has been established. 
 
# Command availability 

CLI resource: modem/Secondary Ethernet

Uplogix system: All

LMS offerings: All

# Syntax 

```
config vpn
```

# Usage 

VPN type is ipsec or pptp.

```
[admin@A505100087 (modem)]# config vpn
--- Existing  Values ---
VPN Type: none
Change these? (y/n) [n]: y
--- Enter New Values ---
VPN Type [none]: pptp
PPTP Server Hostname or IP: 198.6.1.2
User Name: adent
Password: *******
Confirm Password: *******
MPPE Required (y/n) [n]:
Do you want to commit these changes? (y/n):
```

```
[admin@UplogixLM (modem)]# config vpn
--- Existing  Values ---
VPN Type: none
Change these? (y/n) [n]: y
--- Enter New Values ---
VPN Type [none]: ipsec
Vendor [cisco]:
IPsec Server Hostname or IP: 198.6.1.2
IKE DH Group [dh2]:
Perfect Forward Secrecy [server]:
NAT Traversal Mode [none]: cisco-udp
NAT UDP Port [0]: 10000
Allow Single DES (y/n) [n]:
Deny MD5 (y/n) [n]:
Group ID: IPSEC-GROUP
Shared key: *******
Confirm shared key: *******
User Name: adent
Password: *******
Confirm Password: *******
Do you want to commit these changes? (y/n):

```

# In the Uplogix web interface

**Inventory > Local Manager page > Out-of-Band > VPN**  - specific to this system

# History 

3.2 - This command was introduced; it replaces config pptp.

3.3 - Added IPsec support.

3.5 - Added Netscreen VPN endpoint

4.1 - Added DES option

4.5 - Added additional key exchange types for IKE and PFS

# Related commands 

**show vpn**
