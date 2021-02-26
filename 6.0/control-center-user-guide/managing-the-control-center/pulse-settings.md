<!-- 5.4 -->
<div class='warning' />The following instructions are for customers comfortable with the Linux operating system. If you are unsure about any of the commands below, please contact Uplogix Support.</div>

To configure the Control Center as a Pulse server, you will need to enable the echo component of the xinetd daemon. You will also need an IP address to bind the server to.

# Choosing an IP address

It is recommended that you use a secondary IP address on your Control Center if you intend to use it as a Pulse server. The reason has to due with the routing table on your Local Manager.

Here is a simplified example configuration for appliance100:

```
IP Address: 172.30.151.100
Subnet Mask: 255.255.255.0
Default Gateway: 172.30.151.254
EMS IP: 172.30.161.18
Pulse IP: 172.30.161.18
```

During normal operation, the Local Manager has two entries in its routing table.

```
172.30.151.0/24 is a connected network
0.0.0.0 goes to 172.30.151.254 as a default route
```

When the Local Manager goes out of band, it gains a new connected network and its default route changes.

```
172.30.151.0/24 is connected via interface eth3
66.192.168.0/24 is connected via interface ppp0
0.0.0.0 goes to 66.192.168.254 as a default route
```

Since the Local Manager is using Pulse as an indicator of network connectivity, it must continue to contact the Pulse server even while out of band. If the Pulse server begins to respond (network connectivity is restored), then the PPP connection will be turned off.  To ensure that we test the correct link, we add another static route so that requests to the Pulse server will go out the proper interface.

```
172.30.161.18/32 goes to eth3
```

At this point, the Local Manager is operating out of band and is sending Pulse requests through the eth3 interface.  However, that link is still down.

The problem with this setup is that the Local Manager is always trying to contact the Control Center, even when out-of-band.  Although the Local Manager may have a working network path to the Control Center thanks to the out-of-band connection, it won't be able to route to it because of the static .18 route in its routing table.  **It will try to contact the Control Center through the eth3 interface, instead of the ppp0 interface.**

If our Pulse IP had been 161.19, then the Control Center heartbeat request wouldn't have matched the static route and would have succeeded.

# Create a sub-interface on eth0
**Note:** Most Control Centers now have an eth1 interface by default, especially in virtual environments. In those cases, use eth1 as the secondary interface and do not create a sub-interface.

Choose another IP address in the same network and configure a subinterface for eth0.

Log into your Control Center and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root).

Create the ifcfg-eth0:1 under **/etc/sysconfig/network-scripts** file if it does not exist.

```
[root@UplogixControlCenter ~]# cd /etc/sysconfig/network-scripts
[root@UplogixControlCenter network-scripts]# touch ifcfg-eth0:1
```

Edit ifcfg-eth0:1 and add the following two lines. Change the IP line to your secondary IP address. In our example, the Control Center will have an IP address of 198.51.100.1. The Pulse server will be active on 198.51.100.2. 

Save the file.

```
[root@UplogixControlCenter network-scripts]# cat ifcfg-eth0:1
ONBOOT=yes
IPADDR=198.51.100.2
```

Restart network services

```
[root@UplogixControlCenter network-scripts]# service network restart
Shutting down interface eth0:  [  OK  ]
Shutting down loopback interface:  [  OK  ]
Setting network parameters:  [  OK  ]
Bringing up loopback interface:  [  OK  ]
Bringing up interface eth0:  [  OK  ]
```

# Enable the echo service

```
[root@UplogixControlCenter network-scripts]# cd /etc/xinetd.d/
[root@UplogixControlCenter xinetd.d]# vi echo-stream
```

Edit echo-stream and change the bind address to your secondary IP. Also change disable to equal no. Save the file.

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
[root@UplogixControlCenter xinetd.d]# service xinetd restart
Stopping xinetd: [  OK  ]
Starting xinetd: [  OK  ]
```

# Test the echo service

```
[root@UplogixControlCenter xinetd.d]# telnet 198.51.100.1 7
```

Characters should echo when you type them.

> The Control Center may attempt a reverse lookup on the incoming echo request. If there are no nameservers listed in /etc/resolv.conf, a delay may be introduced. This delay may be interpreted by the requesting appliance as a failure.

# Setup complete

You should now be able to point your Local Managers at the Control Center's secondary IP address and get Pulse responses. See [Using the Pulse Feature](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/using-the-pulse-feature) for more information.