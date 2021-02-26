<!-- 5.4 -->

This command invokes the packet capture ability of the Uplogix Local Manager.  The secondary Ethernet port can be configured to monitor a SPAN port of a switch and capture packets matching a variety of conditional statements.  Only the packets destined for the secondary Ethernet port meeting the regular expressions defined in the conditional statements are captured.

A single capture is available to view in text mode or it can be transferred to another system in text or pcap form.   

The capture will spool up to 5 meg of capture detail.  

# Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
usage: capture [options]

--- options ---

  -size <arg>   [integer]

    capture -size 1514


  Expressions:
      host 10.10.10.10 | net 10.10.10.0/24 | port 80

      capture host 10.10.10.90 and port 80 or 443

  Direction source or destination
      src or dst | src | dst | src and dst

      capture src 10.1.1.1 and dst port 80 and 443 or 8443

  Protocol:
      ip | Ip6 | icmp | arp | udp | tcp [portrange] | vlan

      capture ip6 -size 1514 src 2001:470:b851:10:0:0:0:19 and dst port 80
      capture tcp dst portrange 20-21

  Packet size:
      greater | less

      capture greater 1024
      capture less 68

```

# Usage 

```
[admin@UplogixLM]#capture ip6 -size 1514 src 2001:470:b851:10:0:0:0:19 and dst port 80
```

# History
 
4.4 - This command was introduced

# Related commands 

* **show capture** 