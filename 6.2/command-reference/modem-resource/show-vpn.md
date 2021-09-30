<!-- 5.4 -->

Displays the Uplogix Local Manager's VPN configuration.

# Command availability 

CLI resource: modem

Uplogix system: All

LMS offerings: All

# Syntax 

```
show vpn
```

# Usage 

```
[admin@UplogixLM (modem)]# show vpn
VPN type: pptp
User Name: xyzcoAus01
Pptp server ip: 66.193.254.226
MPPE required: yes
40 bit encryption refused: yes
128 bit encryption refused: yes
Stateless encryption refused: yes
```

# In the Uplogix web interface

**Inventory > Local Manager page > Out-of-Band > VPN** - specific to this system

# History 

3.2 - This command was introduced; it replaces show pptp.

# Related commands 

- **config vpn**