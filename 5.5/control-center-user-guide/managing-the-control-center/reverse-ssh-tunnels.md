<!-- 5.4 -->

Some deployments may encounter a situation where Local Managers are placed in a network where the LM is able to initiate a connection to the Control Center (for heartbeat), but connections to the LM are not possible. This could be caused by NATs, firewalls, or simply being on a private network.

To overcome this limitation, a Reverse SSH Tunnel can be initiated from the Local Manager to the Control Center. If a user's connection is proxied through the Control Center, the connection can then piggyback on the tunnel to reach the Local Manager.

# Control Center Configuration

<div class='ucc' />Administration > Server Settings > Reverse SSH Tunnel Settings</div>
![Uplogix Control Center Reverse SSH Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-server-settings-reverse-ssh.png)

The Control Center handles the configuration and synchronization of the Reverse SSH service, so most options are not available for editing. If you need to change the Reverse SSH or Proxy Port, you can edit */etc/sysconfig/embassy.overrides* and add the following lines:

```
MATCH_PORT_SSH=2222
MATCH_PORT_PROXY=2244
```

The default SOCKS 5 Username is *uplogix*. The password is automatically generated during install. If you change these settings, the new information will be synchronized automatically throughout the deployment.  

# Local Manager Configuration

<div class='ucc' />Inventory > Local Manager Summary Page > Network > Reverse SSH</div>

![Uplogix Control Center LM Reverse SSH Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-lm-network-reverse-ssh.png)

## Enabled

Turns on the Reverse SSH service for the Local Manager (or group of Local Managers).

## Limit SSH login to RSSH only

For added security, you can disable the default port 22 SSH service on a Local Manager and limit connections to those initiated through the Reverse SSH tunnel.

## Reverse SSH Server Port

If you changed the Server Port on the Control Center's Reverse SSH server, enter it here (**this is not common**).

## SSH Keep-Alive Seconds

Specify how often the Local Manager should send a keep-alive packet to ensure the connection stays up. **You should not need to change this value.**

## SSH Keep-Alive Bytes

Specify the size of the keep-alive packet. **You should not need to change this value.**

## SSH Client Fingerprint

For reference, the SSH client fingerprint is displayed after this feature is enabled.

# Usage

Enabling this feature automatically synchronizes all necessary information between the Control Center and the Local Manager. 

> This feature is separate from the SS5 SOCKS proxy and does not require it to be present or configured.

Click on the SSH button on the Local Manager Summary page to initiate a connection. The Applet will automatically connect to the Reverse SSH proxy on the Control Center, which will then connect the Applet to the Local Manager via the Reverse SSH tunnel.

# Viewing tunnel status

To view the status of the Reverse SSH tunnel, log into the Local Manager and run the **show system reverse-ssh** command.

```
[super@UplogixVLM]# show system reverse-ssh
Enabled: true
Limit SSH login to RSSH only: no
Reverse SSH server port: 2222
SSH keep-alive seconds: 90
SSH keep-alive bytes: 32

Remote: 198.51.100.1:2222
Active: 47 minutes, 53 seconds
Local: 198.51.100.48:36169 (47:53)
```

# Disabling Reverse SSH Tunnels

By default, the Control Center will listen for Reverse SSH connections on port 2222. If you will not be using Reverse SSH and would like to close port 2222, you can do so by [becoming root](https://uplogix.com/docs/control-center-user-guide/managing-the-control-center) and issuing the following commands:

```
[emsadmin@UplogixControlCenter ~]$ sudo su -
[sudo] password for emsadmin: 
[root@UplogixControlCenter ~]# service matchmaker stop
Shutting down Uplogix MatchMaker: Waiting for Uplogix MatchMaker to exit...
                                                           [  OK  ]
Stopped Uplogix MatchMaker.
[root@UplogixControlCenter ~]# chkconfig matchmaker off
```

The **service** command turns off the Reverse SSH service. The **chkconfig** command prevents the Reverse SSH service from starting after a reboot.