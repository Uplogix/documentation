<!-- 5.4 -->
The Control Center is designed to receive and respond to requests from Local Managers. The following inbound ports are used during normal operation.

* TCP 443 - HTTP, provides access to the Control Center GUI - **required**
* TCP 8443 - Heartbeat and Archive, used for communication between Control Center and Local Managers - **required**
* TCP 7 - Echo, used by the [Pulse](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/using-the-pulse-feature) feature
* TCP 22 - SSH, used to connect to the Control Center CLI
* TCP 2222 - Reverse SSH, used by Local Managers to create a reverse-ssh tunnel with the Control Center <span class="badge">5.4</span>
* TCP 2244 - Reverse SSH, used by clients to connect to Local Managers via the reverse-SSH tunnel <span class="badge">5.4</span>
* TCP 80 - HTTP, provides access to the Control Center GUI, redirects to 443
* UDP 123 - NTP, provides NTP servers to managed devices

If you will be using the SOCKS proxy server, you will also need to open TCP 1080 (typical default) or TCP 9000 (as suggested in our documentation).

> This information is for use with external firewalls and NATs. The Uplogix Control Center runs its own firewall to ensure only the above ports are accessible.

## Traffic Compression

The use of network traffic compression services / devices is not recommended for Uplogix products. Devices such as Riverbed accelerators / optimizers may cause Heartbeat and Pulse features to fail.

Uplogix recommends adding exceptions for the ports listed above to ensure proper operation.