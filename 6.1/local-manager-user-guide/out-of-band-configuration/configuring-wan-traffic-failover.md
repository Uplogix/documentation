<!-- 5.4 -->

# Overview

An Uplogix Local Manager (LM) can provide backup cellular WAN services for a remote site by sharing its out-of-band cellular LTE connection with the local router, firewall or WAN accelerator. This article provides an overview of how our WAN Traffic Failover (WTF) feature works and demonstrates how to configure the Uplogix LM in order to implement this feature.

# Assumptions

This document makes the following two assumptions:

 1. The cellular modem is configured and working
 2. The Local Manager's secondary Ethernet interface (GE-1) is connected to a routed interface on the router or routing device.

# Configuration

## Pulse Configuration

The Local Manager uses the Pulse feature to test in-band network connectivity by sending a TCP echo every 30 seconds to up to three echo servers. You can configure the Local Manager to respond to a loss of connectivity - defined as no response for four consecutive pulses - by initiating an out-of-band connection over the cellular modem and back into your network in order to restore connectivity to the remote site.  Therefore, the pulse feature is used to establish the cellular out-of-band connection for local traffic when WAN connectivity fails.

If the pulse settings are not yet configured, click on the Out-of-Band->Pulse link in the configuration menu on the left side of the Local Manager page to configure pulse settings.  Be sure to enable pulse, point it to at least one pulse server and to "Enable Out-of-Band on Pulse Failure."  Be sure to click the **Save** button to commit the configuration change.

![](http://uplogix.com/support/docs/img/rob/WTF-0-Pulse.png)

> Make sure TCP port 7 is opened up in any firewalls along the path
 between the Local Manager and all pulse servers.

Ideally, the local routing device is configured to not forward pulse traffic through its WTF interface (to the LM) in order to prevent pulse from succeeding over the WTF connection. If this is not possible, the **Remain Out-of-Band on Pulse Success** box can be checked and some **Maximum Time Out-of-Band in Minutes** can be specified so the LM remains out-of-band for that period of time.  Once the maximum time is reached with pulse succeeding, the LM will bring down the modem connection and attempt to communicate via the inband network.  If pulse fails again, the LM will bring the out-of-band modem connection back up for the maximum period of time.

## PPP Configuration

PPP should already be configured since we assumed an installed and working cellular modem.  Therefore, the only PPP configuration that must be made for WTF is to check the box for "Enable Out-of-Band Sharing".

Click on the Out-of-Band->PPP link in the configuration menu on the left side of the Local Manager page to configure PPP settings.  Enable Out-of-Band sharing and click the **Save** button to commit the configuration change.

![](http://uplogix.com/support/docs/img/rob/WTF-1-PPP.png)

## Secondary Ethernet Configuration

The Local Manager Secondary Ethernet port is labeled GE-1 on the front of the Uplogix 500 and 5000 platforms.  This port can function in several roles - one of which is to receive and forward traffic over the Local Manager cellular modem connection for the WAN Traffic Failover feature during a WAN/primary network failure. This article assumes that GE-1 is connected to the local routing device that will failover to the Local Manager either directly or indirectly via the LAN, and that the layer 3 interface on the routing device is configured to either DHCP its IP address, or has been configured with the following static address that it would get via DHCP from the Local Manager:  169.254.100.254/30.

Click on the Network->Secondary Ethernet link in the configuration menu on the left side of the Local Manager page to configure secondary Ethernet for WAN Traffic Failover (WTF).  Perform the following actions: 

 1. Set the secondary Ethernet **Type** to **dhcpserver** 
 2. Check the **Forward traffic over Out-of-Band Connection** box to forwarding ingress traffic on the secondary Ethernet port over the out-of-band modem connection.
 3. Click the **Save** button to commit the configuration changes. 

![](http://uplogix.com/support/docs/img/rob/WTF-2-SecondaryEthernet.png)