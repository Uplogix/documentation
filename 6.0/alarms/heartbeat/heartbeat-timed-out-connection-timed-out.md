# Description

This alarm is to notify you that the heartbeat from the Local Manager the Control Center has failed due to a connection time out. 

# Steps to Resolve

The steps to clear the alarm involve determining the point of failure between the Local Manager and the Control Center.

## Is the network down?

Ping the Control Center IP address to ensure the Local Manager can route to it:

```
[admin@Test5000]# ping 172.30.111.192
PING 172.30.111.192 (172.30.111.192) 56(84) bytes of data.
64 bytes from 172.30.111.192: icmp_seq=1 ttl=62 time=0.364 ms
64 bytes from 172.30.111.192: icmp_seq=2 ttl=62 time=0.371 ms
64 bytes from 172.30.111.192: icmp_seq=3 ttl=62 time=0.399 ms
64 bytes from 172.30.111.192: icmp_seq=4 ttl=62 time=0.391 ms

--- 172.30.111.192 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2998ms
rtt min/avg/max/mdev = 0.364/0.381/0.399/0.019 ms
```

If you are unable to reach the Control Center, it's a good indication that the heartbeat failed due to internal network connectivity issues.

## Is a firewall blocking port 8443?

Heartbeating occurs over port 8443. If you have a firewall on your network, verify that it's allowing transmission of data on port 8443. 


## Are the management configuration settings correct?

Often the error occurs due to incorrect configuration settings. Please see <a href="http://uplogix.com/docs/local-manager-user-guide/system-configuration/control-center-management">Control Center Management</a> and verify that the management configurations settings are correct.

If you are using a DNS server, this alarm can also mean that the DNS server can't be reached. Run the **config system ip** command and verify that the DNS settings are configured correctly.

If these steps do not resolve the issue, please contact Uplogix Support for further troubleshooting steps.



