# Description

[Pulse](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/using-the-pulse-feature) is a feature used to indicate whether or not the Uplogix Local Manager has good network connectivity. If Pulse fails 3 times in a row, the LM can be configured to automatically bring up its out-of-band solution. This alarm is an indication that either the appliance doesn't have a route to the pulse server or the pulse settings are not configured correctly.

# Steps to Resolve
Assuming that Pulse is configured correctly on the Uplogix Local Manager and was working previously, the steps to clear the alarm involve determining the point of failure from the appliance to the Pulse server.

## Is the network down?

Ping the Pulse server to ensure the appliance can route to it:

```
[User@uplogixLM]# ping 172.30.105.1
PING 172.30.105.1 (172.30.105.1) 56(84) bytes of data.
64 bytes from 172.30.105.1: icmp_seq=1 ttl=62 time=0.796 ms
64 bytes from 172.30.105.1: icmp_seq=2 ttl=62 time=0.710 ms
64 bytes from 172.30.105.1: icmp_seq=3 ttl=62 time=0.633 ms
64 bytes from 172.30.105.1: icmp_seq=4 ttl=62 time=0.718 ms

--- 172.30.105.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3001ms
rtt min/avg/max/mdev = 0.633/0.714/0.796/0.060 ms
```

If you are unable to reach the Pulse server via ping, it's a good indication that Pulse is failing due to internal network connectivity issues.

## Is a firewall blocking the echo packets?

If you have a firewall on your network, verify that it's allowing the transmission of echo packets on port 7.

## Is your network security configured on a router or a switch that is blocking echo packets?

Check your network security configuration and verify that a router or switch is allowing echo packets through on port 7.

## Is the Local Manager using the Control Center's secondary IP address as a Pulse server? Verify that the pulse server is running on the UCC.

If you are using your Control Center's secondary IP address as a Pulse server, please see Enable Pulse Server on a Control Center to verify that it is configured correctly.

If it is configured correctly, run a tcpdump on the Control Center to see if it is receiving pings:

Log into your Control Center as emsadmin

1. Run sudo su - to become root. Use emsadmin's password when prompted
2. Run tcpdump ip proto \icmp
3. You should see output like this if the packets are being sent:

```
[root@Uplogix-Production-EMS ~]# tcpdump ip proto \icmp
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), capture size 96 bytes
13:55:36.066556 IP support.uplogix.local > uplogixems.uplogix.local: icmp 64: echo request seq 1
13:55:36.067708 IP uplogixems.uplogix.local > support.uplogix.local: icmp 64: echo reply seq 1
13:55:37.065556 IP support.uplogix.local > uplogixems.uplogix.local: icmp 64: echo request seq 2
13:55:37.065579 IP uplogixems.uplogix.local > support.uplogix.local: icmp 64: echo reply seq 2
13:55:38.064593 IP support.uplogix.local > uplogixems.uplogix.local: icmp 64: echo request seq 3
13:55:38.064606 IP uplogixems.uplogix.local > support.uplogix.local: icmp 64: echo reply seq 3
13:55:39.063637 IP support.uplogix.local > uplogixems.uplogix.local: icmp 64: echo request seq 4
13:55:39.063649 IP uplogixems.uplogix.local > support.uplogix.local: icmp 64: echo reply seq 4
```

If you are not seeing this output, it is a good indication that either Pulse is not configured correctly on the UCC or something is blocking echo packets on port 7.

Please contact Uplogix Support if you are unable to clear the alarm after following the above steps.