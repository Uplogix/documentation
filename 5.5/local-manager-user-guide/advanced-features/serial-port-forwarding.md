<!-- 5.4 -->

Use the Serial Port Forwarding feature to make the console port of the managed device available on a local workstation via reverse SSH tunnel. In order to utilize this feature, a user must have the terminal privilege.

An SSH client with reverse tunnel capabilities is required to use this feature. Supported clients include PuTTY and the SSH Applet on the Control Center.

Prior to setting up serial port forwarding, initialize the Local Manager port with the appropriate device driver via the **config init** command.

# Usage Notes

* Only one telnet connection is allowed per forwarded port. Subsequent connections will fail until the first connection is exited.
* The telnet connection can be terminated by quitting the telnet command, exiting the terminal session on the original SSH session, or by closing the SSH client.
* Accessing a forwarded port via telnet bypasses authentication and authorization. These are handled by the original SSH session.
* Connections to forwarded ports are subject to the same idle timeouts as normal terminal sessions. The idle counter is reset if data is passed over the telnet connection.

# PuTTY

The following is an example using PuTTY, for an example using the SSH Applet in the Control Center, refer to [Serial Port Forwarding](http://uplogix.com/docs/control-center-user-guide/applet/serial-port-forwarding) in the Control Center User Guide.

To set up serial port forwarding using PuTTY:

Open PuTTY to display the configuration window. Enter the IP address of the Uplogix device (1). Under Category on the left, expand the SSH group and select Tunnels (2). 

![Putty - IP and Tunnels](http://uplogix.com/support/docs/img/5.4/putty-ip-tunnels.png)

For Source Port, enter the local TCP port to forward the console connection to (1). This port should not be in use on your computer.

> Windows typically reserves ports 1023 and below. Choose a TCP port number above this range.

For Destination, enter **serialportX_Y:Z** where X is the slot number, Y is the port number, and Z is an arbitrary port number (2).

Leave all other options as default and click Add (3).

![Putty - Serial Port Forwarding](http://uplogix.com/support/docs/img/5.4/putty-serial-port-forwarding.png)

> Be sure to use **serialportX_Y** and NOT **portX_Y**, which is used for [SSH Port Forwarding](http://uplogix.com/docs/local-manager-user-guide/advanced-features/ssh-port-forwarding).

Click Open to begin the SSH session. Enter your username/password and navigate to the port you wish to forward. Use the **terminal forward** command to begin a forwarded session.

```
[admin@UplogixLM]# port 1/4
DAL-CORE cisco 7604 IOS 12.2
[admin@u3200 (port1/4)]# terminal forward
Press ~[ENTER] to exit
Connecting ...
Retrieving running-config from device ...
Complete. running-config pulled.
running-config saved to archive as current.
Console session forwarded.
DAL-CORE#
```

The console port of the managed device is now available locally. Telnet to 127.0.0.1 (localhost) on the Source TCP port specified.

![Putty - Telnet Localhost](http://uplogix.com/support/docs/img/5.4/putty-telnet-localhost.png)

> If you select *Telnet* as the Connection type AFTER entering the port number, PuTTY may change the port back to 23. Be sure to change it to the Source TCP port specified earlier before clicking *Open*.

Anything typed in the telnet session will be visible on the original SSH session.