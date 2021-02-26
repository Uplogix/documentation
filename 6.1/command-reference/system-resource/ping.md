<!-- 5.4 -->

Execute an ICMP echo request from the Uplogix Local Manager to a specific IP address. From the port context, this command attempts to ping the dedicated device IP address. If the dedicated device IP address is not configured, it will attempt to ping the management IP address. 

# Command availability 

CLI resource: system, port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Uplogix system: All

LMS offerings: All

# Syntax

```
ping <â€œip addressâ€ | -m>
ping <ipv6 address>
```

From the system context, specify an IP address to ping.

From the port context, specify **-m** to ping the management IP address if there is a dedicated Ethernet configured.

# Usage 

Only specific IP addresses (no broadcast) are supported.

Default routes are used (Management Ethernet or PPP/VPN if active).

```
[admin@UplogixLM]# ping 172.230.53.20
PING 172.230.53.20 (172.230.53.20) 56(84) bytes of data.
64 bytes from 172.230.53.20: icmp_seq=1 ttl=64 time=0.265 ms
64 bytes from 172.230.53.20: icmp_seq=2 ttl=64 time=0.228 ms
64 bytes from 172.230.53.20: icmp_seq=3 ttl=64 time=1.25 ms
64 bytes from 172.230.53.20: icmp_seq=4 ttl=64 time=0.216 ms
--- 172.230.53.20 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2999ms
rtt min/avg/max/mdev = 0.216/0.489/1.250/0.440 ms
```

# History 

2.1 - Command available from port menu.

# Related commands 

- **device ping**
