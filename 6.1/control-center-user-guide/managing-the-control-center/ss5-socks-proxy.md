# Overview

The Uplogix Control Center comes pre-installed with a SOCKS proxy called SS5. Follow the steps below to enable this service.

# Configure SS5

Access your Control Center as emsadmin and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root). Change directory to /etc/opt and make the ss5 directory world-executable.

```
[root@UplogixControlCenter ~]# cd /etc/opt
[root@UplogixControlCenter opt]# chmod a+x ss5
```
Change directory to /etc/opt/ss5 to configure SS5.

```
[root@UplogixControlCenter opt]# cd ss5
[root@UplogixControlCenter ss5]#
```

Edit the ss5.conf file and replace everything with the following config.

```
[root@UplogixControlCenter ss5]# cp ss5.conf ss5.conf.bak
[root@UplogixControlCenter ss5]# vi ss5.conf
-- output removed --
[root@UplogixControlCenter ss5]# cat ss5.conf
#set SS5_VERBOSE
#set SS5_DEBUG
auth 0.0.0.0/0 - u
permit u 0.0.0.0/0 - 0.0.0.0/0 - - - - -
```

Edit the ss5.passwd file to set a username and password.

```
[root@UplogixControlCenter ss5]# cat ss5.passwd
username password
```

Be sure to choose a strong password.

Edit the /etc/sysconfig/ss5 file so it includes the IP address and Port you want to bind to.

In this example, the Control Center's IP is 198.51.100.1 and we will be listening on port 9000.

```
[root@UplogixControlCenter ss5]# cat /etc/sysconfig/ss5
# Add startup option here
#SS5_OPTS=" -u root"
SS5_OPTS=" -b 198.51.100.1:9000"
```

The above example is the preferred configuration for SS5. However, if you wish to run the proxy server on a port lower than 1024, you will need to run SS5 as root. The configuration looks like this:

```
[root@UplogixControlCenter ss5]# cat /etc/sysconfig/ss5
# Add startup option here
#SS5_OPTS=" -u root"
SS5_OPTS=" -u root -b 172.30.151.200:81"
```

This completes the SS5 configuration.

# Configure nftables
You will need to add an exception to the UCC's firewall before users will be able to connect to the proxy server.

Edit **/etc/sysconfig/nftables.conf** and add port 9000 (or the port you configured) to the following section:

```
set tcp_accepted {
                type inet_service; flags interval;
                elements = {
                        7, 22, 80, 2222, 2244, 443, 8443
                }
        }
```

It should look like this:

```
set tcp_accepted {
                type inet_service; flags interval;
                elements = {
                        7, 22, 80, 2222, 2244, 443, 8443, 9000
                }
        }
```				

Restart the nftables service.

```
[root@UplogixControlCenter ss5]# systemctl restart nftables
[root@UplogixControlCenter ss5]#
```

This completes the nftables configuration.

# Start SS5

Use the service command to start, stop, and restart the SOCKS proxy server.

```
[root@UplogixControlCenter ss5]# service ss5 start
Starting ss5
done                                                       [  OK  ]
[root@UplogixControlCenter ss5]# service ss5 restart
Restarting ss5...  
done                                                       [  OK  ]
Shutting down ss5...
done                                                       [  OK  ]
[root@UplogixControlCenter ss5]# service ss5 stop
Shutting down ss5... 
done                                                       [  OK  ]
```

# Configure Control Center

You are now ready to configure the Applet settings on your Control Center. 

Consult the [SOCKS Proxy](http://uplogix.com/docs/control-center-user-guide/applet/socks-proxy) topic for more information.