<!-- 5.4 -->

Shows the capture of network traffic via the Secondary Ethernet interface for troubleshooting purposes.

To enable capture mode, run **config system secondary** from the system resource and specify capture as the type.


# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax

```
show capture
```

# Usage

```
[admin@UplogixLM]# show capture
18:53:25.281292 CDPv2, ttl: 180s, Device-ID '333A'[|cdp]
18:53:25.284526 CDPv2, ttl: 180s, Device-ID '333A'[|cdp]
18:53:25.287029 CDPv2, ttl: 180s, Device-ID '333A'[|cdp]
18:53:25.926118 802.1d config TOP_CHANGE 8000.00:d0:ba:bf:62:cd.8022 root
2000.00:d0:01:c1:c4:34 pathcost 23 age 3 max 20 hello 2
fdelay 15
18:53:26.315752 IP6 :: > ff02::16: HBH ICMP6, multicast listener report v2, 1 group
record(s), length 28
18:53:26.391749 IP6 :: > ff02::1:ff00:1524: ICMP6, neighbor solicitation, who has
fe80::20f:2cff:fe00:1524, length 24
18:53:26.942055 802.1d config TOP_CHANGE 8000.00:d0:ba:bf:62:cd.8022 root
2000.00:d0:01:c1:c4:34 pathcost 23 age 2 max 20 hello 2
fdelay 15
18:53:27.391840 IP6 fe80::20f:2cff:fe00:1524 > ff02::2: ICMP6, router solicitation,
length
16
18:53:28.358245 802.1d config TOP_CHANGE 8000.00:d0:ba:bf:62:cd.8022 root
2000.00:d0:01:c1:c4:34 pathcost 23 age 2 max 20 hello 2
fdelay 15
```
To export the capture file in pcap format, use **show capture -pcap** and pipe it to SCP, FTP, or Email.

To export via SCP, use the following syntax:

```
[admin@UplogixLM]# show capture -pcap | scp uplogix@192.0.2.226:uplogixlm.cap1
uplogix@192.0.2.226's password:*******
..
File successfully sent to 192.0.2.226.
copy succeeded
```
In the above example, the capture file will be attached to the email with the filename uplogixlm.cap1. The file can then be viewed in any third party application capable of reading pcap files (Wireshark, etc.).

To export the capture file in plain text with SCP, FTP, or Email, simply omit the -pcap option.

# In the Uplogix web interface

To enable capture mode:

**Inventory > group page > Network > Secondary Ethernet** - specific to this inventory group

**Inventory > Local Manager page > Network > Secondary Ethernet** - specific to this system

#Related commands

- **capture**
- **config sys secondary**


