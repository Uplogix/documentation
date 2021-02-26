Most of the Local Managerâ€™s communication is designed to be initiated by the Local Manager, reducing the number of potential security vulnerabilities. These operations are discussed in detail below.

# Archiving and exporting

If the Local Manager is managed by a Control Center, the Local Manager periodically archives SLV statistics, user session log files, device files, and other data automatically to the Control Center using HTTPS over port 8443. Archiving uses high data compression to reduce the impact to the network. When operating out-of-band, archiving is suspended by default until the Local Manager returns to in-band communication. This functionality can be enabled to work when the Local Manager is communicating over its out-of-band connection.

A Local Managerâ€™s configuration can be retrieved using the **config export** command to create an XML file of its config and send it to the IP address of your choice using SCP or FTP. Use the **config system export** command to archive collected device statistics to an external server using FTP or SCP.

# Pulse

The Pulse client uses the ECHO protocol (TCP port 7) to determine network availability. TCP ECHO packets are sent every 30 seconds from the management Ethernet port to one or more pulse servers (usually in the Network Operation Center or on the other side of the WAN). The in-band/production network is deemed down after four consecutive ECHO failures from all defined pulse servers, after which the Local Manager can automatically initiate an out-of-band connection over the modem or secondary Ethernet port to reestablish connectivity to the remote site.

While out-of-band, the Local Manager routes all traffic over the out-of-band connection except for ECHOs destined for the pulse server and for local traffic as defined by the user with the **config system route** command. The Local Manager will automatically tear down the out-of-band connection and communicate over the in-band/management Ethernet connection when it sees that the in-band network is operational again (determined by five consecutive successful echo requests).

# Heartbeat

The Local Manager communicates with the Control Center using a proprietary TLS-encrypted protocol that uses TCP port 8443 to provide regular updates that include current device status information, status of scheduled jobs, alarms, events and configuration changes on the Local Manager. The message that is sent by the Local Manger to the Control Center and that is acknowledged by the Control Center is called the heartbeat. The heartbeat contains compressed data to reduce the load on the network and has a 30 second interval by default.

You can change the heartbeat interval and TCP port from the command line using the **config system management** command.

# Network Time Protocol

If this feature is enabled, the Local Manager will synchronize time with a Network Time Protocol (NTP) server using UDP port 123. If the Local Manager is used with the Control Center, it will sync its time over the heartbeat with the Control Center by default. The Local Manager can be configured to sync its time with an NTP server instead of the Control Center using the **config system ntp** command.

# Reverse SSH

If [Reverse SSH](https://uplogix.com/docs/control-center-user-guide/managing-the-control-center/reverse-ssh-tunnels "Reverse SSH") is enabled, the Control Center will listen for connections from the Local Manager on TCP port 2222*. The Local Manager will maintain a persistent connection that is used to tunnel SSH from a user workstation to an LM.

Additionally, TCP port 2244* is used by end users to connect their workstation through the Control Center to the Local Manager over the Reverse SSH tunnel.

# TACACS/RADIUS Authorization

If a [third-party AAA](https://uplogix.com/docs/control-center-user-guide/accounts-and-security "Third-party AAA") server is used, for RADIUS servers the default port is UDP 1645 or 1812; for TACACS, the default port is TCP 49.

# Syslog

If a [third-party syslog](https://uplogix.com/docs/control-center-user-guide/accounts-and-security "third-party syslog") server is used, the default port is UDP port 514*.  Each device port can point to a different IP, UDP port or facility.

# VPN (outband only)

If a [third-party VPN](https://uplogix.com/docs/control-center-user-guide/accounts-and-security "third-party VPN") server is used in outband mode to additionally encrypt and tunnel traffic, GRE, Ikev1 and Ikev2 IPSEC tunnels are supported.

* **GRE** - TCP 1723 and Protocol 47. 

* **IkeV1 IPSEC** - Cisco UDP - UDP port 10,000*, ESP (Protocol 50), NATT â€“ UDP port 500.

* **IkeV2 IPSEC** - UDP port 500.

# Virtual Port

If a virtual port is configured, both SSH and Telnet are supported on TCP port 22-23*. Each device port can point to a different IP/TCP port.

*Can be customized for your installation.

**Uplogix has reference designs for Cisco ASA/IOS and Palo Alto.