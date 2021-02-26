<!-- 5.4 -->

The Uplogix Control Center comes pre-installed with a SOCKS proxy called SS5. Follow the steps below to enable this service.

# Configure SS5

Access your Control Center as emsadmin and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root). Change directory to /etc/opt and make the ss5 directory world-executable.

```
[root@ems13 ~]# cd /etc/opt
[root@ems13 opt]# chmod a+x ss5
```
Change directory to /etc/opt/ss5 to configure SS5.

```
[root@ems13 opt]# cd ss5
[root@ems13 ss5]#
```

Edit the ss5.conf file and replace everything with the following config.

```
[root@ems13 ss5]# cp ss5.conf ss5.conf.bak
[root@ems13 ss5]# vi ss5.conf
-- output removed --
[root@ems13 ss5]# cat ss5.conf
#set SS5_VERBOSE
#set SS5_DEBUG
auth 0.0.0.0/0 - u
permit u 0.0.0.0/0 - 0.0.0.0/0 - - - - -
```

Edit the ss5.passwd file to set a username and password.

```
[root@ems13 ss5]# cat ss5.passwd
username password
```

Be sure to choose a strong password.

Edit the /etc/sysconfig/ss5 file so it includes the IP address and Port you want to bind to.

In this example, the Control Center's IP is 198.51.100.1 and we will be listening on port 9000.

```
[root@ems13 ss5]# cat /etc/sysconfig/ss5
# Add startup option here
#SS5_OPTS=" -u root"
SS5_OPTS=" -b 198.51.100.1:9000"
```

The above example is the preferred configuration for SS5. However, if you wish to run the proxy server on a port lower than 1024, you will need to run SS5 as root. The configuration looks like this:

```
[root@ems13 ss5]# cat /etc/sysconfig/ss5
# Add startup option here
#SS5_OPTS=" -u root"
SS5_OPTS=" -u root -b 172.30.151.200:81"
```

This completes the SS5 configuration.

# Configure iptables

You will need to open a hole in the firewall before users will be able to connect to the proxy server.

Edit /etc/sysconfig/iptables and add the following lines.

```
-A INPUT -p tcp -m tcp --dport 9000 --tcp-flags SYN,RST,ACK SYN -j ACCEPT
```

Adjust the "dport 9000" value to the port you chose for SS5. Add the line **before the final DROP statement** in iptables.

Restart the iptables service.

```
[root@ems13 ss5]# service iptables restart
Flushing firewall rules: [ OK ]
Setting chains to policy ACCEPT: filter [ OK ]
Unloading iptables modules: [ OK ]
Applying iptables firewall rules: [ OK ]
[root@ems13 ss5]#
```

This completes the iptables configuration.

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