<!-- 5.4 -->
<div class='ucc' />Inventory > Local Manager Summary Page > Network > Proxy</div>

The Control Centerâ€™s CLI applet supports the use of a SOCKS Proxy server when accessing Uplogix devices. Setting up a SOCKS Proxy allows users to access devices through a proxy to bypass routing and firewall limitations and configure proxy servers for groups and/or individual devices.

A properly configured SOCKS Proxy server is required to use this feature. Uplogix Control Centers come pre-installed with the SS5 SOCKS Proxy Server. See [SS5 SOCKS Proxy](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/ss5-socks-proxy) to configure this service.

# Arguments

## Proxy Version

Both SOCKS Proxy Version 4 and 5 are supported.

> SS5 uses version 5 (with authentication)

## Host

The IP address of the SOCKS Proxy Server. Do not use 127.0.0.1 or localhost. The client computer must be able to route to the SOCKS IP address.

## Port

The listening port of the Socks Proxy Server. Typical default port is 1080.

> If you configured the Control Center's SS5 proxy as described in [SS5 SOCKS Proxy](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/ss5-socks-proxy), the port will be 9000.

## Username

Username to authenticate with the proxy server, if required.

## Password

Password to authenticate with the proxy server, if required.

# Usage

Proxy settings can be configured at the global, group, or individual device level.

<div class='ucc' />Inventory > Inventory Group > Network > Proxy</div>
<div class='ucc' />Inventory > Local Manager Summary Page > Network > Proxy</div>

In this example, the Control Center will be configured to use a socks proxy server with the following configuration:

* **Version:** 5
* **IP Address:** 198.51.100.1
* **Port:** 9000
* **Username:** socks_user
* **Password:** Tv6P#z62#&

![Uplogix Control Center Proxy Settings](http://uplogix.com/support/docs/img/6.0/proxy-settings.png)

When the Proxy Version is set to **disabled**, the configuration options will be grayed out. To begin configuring settings, change the Proxy Version to either **4** or **5**.

* **Version 4:** Requires an IP address and a listening port. Since Version 4 does not support authentication, the password field is grayed out.
* **Version 5:** All configuration options are available with this version. Depending on the configuration of the proxy server, a username and password may be required.

Once you have configured necessary settings, click *Save*.

The Socks Proxy configuration will be transparent to the end user. To test your settings, select a previously inaccessible device from the Inventory and launch the SSH applet. A connection to the device should succeed.

If the connection fails, verify that your settings are correct by examining the configuration of the proxy server or by testing with an SSH client such as Putty or SecureCRT.