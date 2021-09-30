# Overview

To make changes to the Control Center's operating system, you will need to log into the Control Center via SSH or a console connection and become root.

The default *emsadmin* user does not have the necessary privileges to make changes to the operating system.

First, log into the Control Center.

```
[user@centos-vm ~]$ ssh emsadmin@198.51.100.1
emsadmin@198.51.100.1's password: 
Last login: Mon Nov 21 13:00:16 2016 from 198.51.100.99
```

Run **sudo su -** to become root and load its environment. Use emsadmin's password when prompted.

```
[emsadmin@UplogixControlCenter ~]$ sudo su -
[sudo] password for emsadmin: 
[root@UplogixControlCenter ~]#
``` 

# Caution

As root, you have the ability to add/remove/change software on the Control Center. Unexpected software may conflict with Uplogix software and cause the Control Center to stop working. Any software not mentioned in Uplogix documentation is considered unsupported.


