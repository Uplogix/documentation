# Description

The Uplogix Control Center and Local managers rely on NTP (Network Time Protocol) to keep their clocks in sync. This alarm is an indication that the appliance is not able to contact a valid NTP server or the NTP settings are not configured correctly.

# Steps to Resolve

## Verify that the Local Manager is pointing to a vaild NTP server

If you are seeing this alarm on a Local Manager, it's most likely due to a problem with the NTP server specified in the command **config system ntp**.

Please see Date and Time to verify that the NTP settings are configured correctly on the Local Manager.

You can also run **show system ntp** and compare those values to a known-good LM (if possible) to see if the configurations match up.

## Verify that NTP settings are configured correctly on the Control Center

Please see Configuring NTP Settings to verify that NTP is configured correctly on the Control Center.

## Verify that there is a route between the appliance and the NTP server

Ping the IP address of the NTP server to verify that the path is valid:

```
[admin@UplogixLM]# ping 172.30.5.201
PING 172.30.5.201 (172.30.5.201) 56(84) bytes of data.
64 bytes from 172.30.5.201: icmp_seq=1 ttl=61 time=33.9 ms
64 bytes from 172.30.5.201: icmp_seq=2 ttl=61 time=33.9 ms
64 bytes from 172.30.5.201: icmp_seq=3 ttl=61 time=33.9 ms
64 bytes from 172.30.5.201: icmp_seq=4 ttl=61 time=33.8 ms


--- 192.168.199.201 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 33.837/33.910/33.954/0.230 ms
```

If you unable to ping the NTP server, it is most likely an indication of internal network connectivity issues. 

Please contact Uplogix Support if you are unable to clear the alarm after following the above steps.