<!-- 5.4 -->

Capture mode allows the capture and review of network traffic via the Secondary Ethernet interface.

* The maximum size of the capture file is 5MB. Collection will automatically stop when this limit is reached.
* Traffic can be captured from a switch port in port monitor mode if the switch is configured correctly.

# Device Configuration

To enable capture mode, run the **config system secondary** command from the system resource and specify capture as the type.

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
[E1] Primary Ethernet Link: yes (bonded active)
[E2] Auxiliary Ethernet Link: no (bonded)
[E3] Internal SFP Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: capture
speed/duplex [auto]: 
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n): y

```

# Capturing Packets (Basic)

To begin capturing packets, use the **capture** command from the system resource. Capture will continue until you press x, CTRL+C, or the 5MB capture limit is reached.

```
[admin@UplogixLM]# capture
Press 'x' or Ctrl+C to stop capturing packets.
4864 bytes
Capture stopped.
```

# Capturing Packets (Advanced)

A variety of options are available to filter captured packets.

 - IP Address capture host 192.0.2.100
 - Network capture net 192.0.2.0/24
 - Port capture port 80
 - IP Address & Port capture host 192.0.2.100 and port 80
 - Source capture src 192.0.2.1
 - Destination capture destination 192.0.2.253
 - Frame Size capture greater 512, capture less 128
 - Bytes Per Frame capture â€“size 32

# Viewing Captured Packets

To view the capture file in plain text, use the **show capture** command.

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

To export the capture file in pcap format, use the **show capture â€“pcap** command and pipe it to SCP, FTP, or Email.

To export via SCP, use the following syntax:

```
[admin@UplogixLM]# show capture -pcap | scp uplogix@192.0.2.226:uplogixlm.cap1
uplogix@192.0.2.226's password:*******
..
File successfully sent to 192.0.2.226.
copy succeeded
```

To export via Email, use the following syntax:
```
[admin@UplogixLM]# show capture -pcap | mailto support@uplogix.com:uplogixlm.cap1
..
File successfully sent to uplogix.com.
copy succeeded
```

In the above example, the capture file will be attached to the email with the filename uplogixlm.cap1. The file can then be viewed in any third party application capable of reading pcap files (Wireshark, etc.).

To export the capture file in plain text with SCP, FTP, or Email, simply omit the â€“pcap option.