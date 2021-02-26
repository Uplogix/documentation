# Overview
This section details the configuration of the Uplogix Control Center as a Pulse (echo) server. These instructions are intended for customers comfortable with the Linux operating system. If you are unsure about any of the commands below, please contact Uplogix Support.

To configure the Control Center as a Pulse server, you will need to enable the echo component of the xinetd daemon. You will also need an IP address to bind the server to.

# Choose a secondary IP address
It is recommended that you use a secondary IP address on your Control Center if you intend to use it as a Pulse server. During normal operation, a static route is created on the Local Manager that directs all traffic to the Pulse server IP through the management interface. If the Pulse server IP and the Management server IP are the same, then heartbeat will always be directed through the management interface, even when the primary network is down and an alternate path is available via an out-of-band connection.

# Configure the secondary interface
The configuration file for the UCC's secondary interface is located at **/etc/sysconfig/network-scripts/ifcfg-net1**.

> CentOS 6: /etc/sysconfig/network-scripts/ifcfg-eth1

This interface should already have been configured using the netSetup script as described in [Provisioning](https://uplogix.com/docs/control-center-user-guide/installation-and-configuration/provisioning). If not, you can manually edit the file to configure the IP address, subnet mask, and default gateway.

To reset network services after configuring net1, use the **systemctl restart NetworkManager** command.

> CentOS6: service network restart

To view the current network configuration, use the **ifconfig** command.

```
[root@UplogixControlCenter network-scripts]# ifconfig | grep net
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
net0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.30.5.184  netmask 255.255.254.0  broadcast 172.30.5.255
        inet6 fe80::20c:29ff:fe1e:ae78  prefixlen 64  scopeid 0x20<link>
        inet6 2001:470:b851:500:20c:29ff:fe1e:ae78  prefixlen 64  scopeid 0x0<global>
        ether 00:0c:29:1e:ae:78  txqueuelen 1000  (Ethernet)
net1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.30.5.185  netmask 255.255.254.0  broadcast 172.30.5.255
        inet6 2001:470:b851:500:20c:29ff:fe1e:ae82  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::20c:29ff:fe1e:ae82  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:1e:ae:82  txqueuelen 1000  (Ethernet)
```

# Enable the echo service
The echo service is part of xinetd. Configuration files are located in **/etc/xinetd.d/**.

```
[root@UplogixControlCenter network-scripts]# cd /etc/xinetd.d/
[root@UplogixControlCenter xinetd.d]# vi echo-stream
```

Edit echo-stream and change the bind address to your secondary IP. Also change disable to equal no. Save the file.

Edit the echo-stream file and make the following changes/additions:

* Change bind IP address to the UCC's secondary IP
* Change disable to no
* Add instances = 1000
* Add cps = 500 30

```
[root@UplogixControlCenter xinetd.d]# cat echo-stream
## default: off
## description: An xinetd internal service which echo's characters back to clients. \
## This is the tcp version.

service echo
{
        type            = INTERNAL
        id              = echo-stream
        socket_type     = stream
        protocol        = tcp
        user            = root
        wait            = no
        bind            = 198.51.100.2
        disable         = no
        instances       = 1000
        cps             = 500 30
}
```

Restart the xinetd service.

```
[root@UplogixControlCenter xinetd.d]# systemctl restart xinetd.service
[root@UplogixControlCenter-Eval xinetd.d]#
```

> CentOS 6: service xinetd restart

# Verify echo service
Verify the echo service is running and bound to the correct IP using the **netstat** command.

```
[root@vUCC-Eval xinetd.d]# netstat -an | grep :7
tcp        0      0 172.30.5.185:7          0.0.0.0:*               LISTEN
```

In the above example, echo is active on port 7 and bound to 172.30.5.185. If no results are returned, or if the bound IP address is listed as 0.0.0.0:7, then something may be misconfigured.
# Test the echo service

```
[root@UplogixControlCenter xinetd.d]# telnet 172.30.5.185 7
```

Type some characters and hit Enter. The same characters should echo back.

> The Control Center may attempt a reverse lookup on the incoming echo request. If there are no nameservers listed in /etc/resolv.conf, a delay may be introduced. This delay may be interpreted by the requesting appliance as a failure.

# Setup complete

You should now be able to point your Local Managers at the Control Center's secondary IP address and get Pulse responses. See [Using the Pulse Feature](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/using-the-pulse-feature) for more information.