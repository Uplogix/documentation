<!-- 5.5 -->

<div class='ucc' />Inventory > Local Manager Summary >Â Out-of-Band > Pulse</div>

# Overview

The Local Manager uses the Pulse feature to test in-band network connectivity by sending 15 bytes of data on TCP port 7 (echo) every 30 seconds to up to three echo servers. You can configure the Local Manager to respond to a loss of connectivity &mdash; defined as no response for four consecutive pulses &mdash; by initiating an out-of-band connection over a modem or the secondary Ethernet management port through an alternate network such as the internet back into your network.

> The echo packets are under 64 bytes to limit impact on the network. The echo is expected to return the exact data sent.

During out-of-band operation, the Local Manager continues sending echo requests to the Pulse server through the in-band connection. When it receives five consecutive echoes, the out-of-band connection is dropped and normal operation resumes. If users are logged in to the Local Manager over the out-of-band connection via SSH, the out-of-band session will persist until all SSH sessions are closed.

> To optionally use the modem's TTY dial-in access feature for out-of-band connectivity, it can be configured to answer only on Pulse failure using the **config answer** command.

To configure the Pulse process, select up to three hosts in your network to be Pulse servers. The hosts should be reliable indicators of good network connectivity. A Control Center can be used as a Pulse server; however, it should be given a secondary IP address for that purpose to provide heartbeat communications over the out-of-band network when the network is down. If the Local Manager cannot communicate with the server, it cannot deliver network data or receive configuration updates. Other common devices that can be used as pulse servers are Cisco routers using the TCP-small-servers service or Windows or Unix systems configured with the echo process enabled.

By default, the Local Manager uses TCP port 7 for the Pulse process and is configurable. Up to three Pulse servers can be configured, enabling Pulse server redundancy.

Use the **config system pulse** command to enter the settings.

```
[admin@UplogixLM]# config system pulse
--- Existing  Values ---
Use Pulse: false
Pulse Server IP 1: 127.0.0.1
Pulse Server Port 1: 7
Pulse Server IP 2: 127.0.0.1
Pulse Server Port 2: 7
Pulse Server IP 3: 127.0.0.1
Pulse Server Port 3: 7
Enable Out-of-Band on Pulse Failure: no
Change these? (y/n) [n]: y
--- Enter New Values ---
Use Pulse (y/n) [n]: y
Pulse IP 1 [172.30.5.44]: 203.0.113.225
Pulse Port 1 [7]:
Pulse IP 2 [127.0.0.1]: 203.0.113.226
Pulse Port 2 [7]:
Pulse IP 3 [127.0.0.1]: 198.51.100.225
Pulse Port 3 [7]:
Enable Out-of-Band on Pulse Failure (y/n) [n]: y
Remain Out-of-Band after Pulse Success (y/n) [n]:
Maximum Time Out-of-Band (minutes; 0 means indefinite) [0]:
Do you want to commit these changes? (y/n): y

```

If you do not want the Local Manager to automatically initiate an out-of-band connection on Pulse failure, be sure to answer **n** to the *Enable Out-of-Band on Pulse Failure (y/n)* question.

If you want the Local Manager to remain out-of-band for some period of time after Pulse starts succeeding again (not a common configuration), be sure to answer **y** to *Remain Out-of-Band after Pulse Success (y/n)* and then indicate how long the Local Manager should remain out-of-band after Pulse starts succeeding again by specifying a time period in minutes to the *Maximum Time Out-of-Band (minutes; 0 means indefinite)* question.  This configuration can be useful when configuring the WAN Traffic Failover feature if the router is not configured to block the Local Manager Pulse traffic from being forwarded over the Local Manager's cellular network connection.

The Pulse server's echo application should comply with RFC 862 such as those provided with Microsoft Windows 2000 Server or Red Hat Linux 7.3.

If the Pulse server does not echo packets for four consecutive attempts, an alarm will be generated.

```
[admin@UplogixLM]# show alarm
UTC   Elapsed Device Context Message 
----- ------- ------ ------- --------------------------------------
18:26 0:32                   Failed to connect to pulse server.
```

# Using the Control Center as a Pulse server

If you'd like to use the Control Center as a Pulse (echo) server, see [Pulse Settings](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/pulse-settings) in the [Control Center User Guide](http://uplogix.com/docs/control-center-user-guide).

