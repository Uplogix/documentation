# Overview 

The Uplogix Control Center and Local Managers rely on NTP to keep their clocks in sync. This keeps timestamps on alarms and events correct and ensure scheduled jobs and monitors run at the right time. If the UCC and LMs are not synchronized, the following alarm will be generated on the Local Manager:

```
System and management server clocks are more than 20 seconds out of sync
```

Control Centers should arrive with their clocks already synchronized to UTC time. Changing to another time zone (or moving the time too far ahead/back) may cause the application to fail.

<div class='danger' />Do not alter the Control Center's time zone.</div>

Part of the Control Center's setup involves pointing it at a valid NTP server. This should keep the clock in sync automatically. However, NTP settings can be configured outside of the setup script if they need to be updated.

Please choose the instructions that match your version of software.
# LMS 6.1 and later (CentOS 8)
Log into the UCC and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root).

> In CentOS 8, ntp has been replaced with [chrony](https://chrony.tuxfamily.org/)

## /etc/chrony.conf

Use **vi** to edit */etc/chrony.conf*.

```
[root@UplogixControlCenter ~]# vi /etc/chrony.conf
```

Look for a line that says *server*, similar to: 

```
server pool.ntp.org iburst
```

If that line doesn't exist, you can add it to the end of the configuration file.

Press the "I" key to enter Insert mode. Replace or add your NTP server IP address or hostname after the *server* command.

```
server 10.10.10.22 iburst
```

Press ESC, then type :wq to save the file.

## Sync the UCC's time

Stop the chronyd service.

```
[root@vUCC ~]# systemctl stop chronyd.service
```

Use the **chronyd** command to synchronize the time.

```
[root@vUCC ~]# chronyd -q 'server pool.ntp.org iburst'
2021-02-11T16:44:19Z chronyd version 3.5 starting (+CMDMON +NTP +REFCLOCK +RTC +PRIVDROP +SCFILTER +SIGND +ASYNCDNS +SECHASH +IPV6 +DEBUG)
2021-02-11T16:44:19Z Initial frequency -13.140 ppm
2021-02-11T16:44:24Z System clock wrong by 0.001404 seconds (step)
2021-02-11T16:44:24Z chronyd exiting
```

Start the chronyd service.

```
[root@vUCC ~]# systemctl start chronyd.service
```

## Check NTP status

You can use the **chronyc sources** command to check the status of NTP synchronization.

```
[root@vUCC ~]# chronyc sources
210 Number of sources = 2
MS Name/IP address         Stratum Poll Reach LastRx Last sample               
===============================================================================
^- 127.127.1.0                   5   6   177    50  +3052ns[+3052ns] +/-  243ms
^* 157.119.108.165               4   6   177    55   -873us[-1155us] +/-  242ms
```

You can use the **chronyc clients** command to view the status of incoming queries.

```
[root@vUCC-Eval ~]# chronyc clients
Hostname                      NTP   Drop Int IntL Last     Cmd   Drop Int  Last
===============================================================================
localhost.localdomain          14      0   6   -    64       0      0   -     -
172.30.5.47                     9      0   2   -     9       0      0   -     -
```

<hr>
# LMS 6.0, 5.5, and 5.4 (CentOS 6)

## Log into the UCC and become root

As with all OS-level configuration, you must first log into the UCC via SSH or console and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root).

## Edit /etc/ntp.conf

The

Use **vi** to open the /etc/ntp.conf file.

```
[root@UplogixControlCenter ~]# vi /etc/ntp.conf
```

Press the "I" key to enter Insert mode. Add the following lines to /etc/ntp.conf, substituting your NTP server's IP address or hostname (if DNS is configured).

```
server 203.0.113.201
restrict 203.0.113.201
```

> If you have not previously run the netSetup.sh script, the "server" line may be missing. Simply add it above "restrict."

Press ESC, then type **:wq** to save the file.

If you are not using NTP Authentication, you can skip to [*Sync the UCC's time*](#sync-the-ucc)

## Enable NTP Authentication (OPTIONAL)

If your NTP server requires authentication through a pre-shared secret, additional configuration is required.

### Update /etc/ntp.conf

Use **vi** to open the /etc/ntp.conf file.

```
[root@UplogixControlCenter ~]# vi /etc/ntp.conf
```

Press the "I" key to enter Insert mode. Modify the "server" and "restrict" lines to match the following syntax, substituting your NTP server's IP. Add the "keys" and "trusted" lines as well.

```
server 203.0.113.201 key 1
restrict 203.0.113.201 notrust

keys /etc/ntp.keys
trustedkey 1
```
Press ESC, then type **:wq** to save the file.

### Create /etc/ntp.keys

Use **vi** to create/open the /etc/ntp.keys file.

```
[root@UplogixControlCenter ~]# vi /etc/ntp.keys
```

Press the "I" key to enter Insert mode. Add the following line, substituting your pre-shared secret.

```
1 M my-preshared-secret
```

**1** specifies the key number. You may have to add multiple keys if you use more than one NTP server and if each has its own key.

**M** specifies an MD5 pre-shared secret.

**my-preshared-secret** can be any word between 1 and 31 characters. It cannot contain any of the following characters:

```
(space), #, \t, \n, \0
```

### Secure /etc/ntp.keys

To ensure only ntp process and root user can read/edit the file, run the following commands:

```
[root@UplogixControlCenter ~]# chmod 640 /etc/ntp.keys 
[root@UplogixControlCenter ~]# chown root:ntp /etc/ntp.keys 
[root@UplogixControlCenter ~]# ls -al /etc/ntp.keys 

-rw-r-----  1 root ntp 12 Jan 25 14:01 /etc/ntp.keys
```

## Sync the UCC's time

Stop the ntpd service.

```
[root@UplogixControlCenter ~]# service ntpd stop
Shutting down ntpd:                                        [  OK  ]
```

Use the **ntpdate** command to synchronize the time.

```
[root@UplogixControlCenter ~]# ntpdate 192.51.100.1
18 Nov 18:29:38 ntpdate[11892]: step time server 192.51.100.1 offset -1.502414 sec
```


Start the ntpd service.

```
[root@UplogixControlCenter ~]# service ntpd start
Starting ntpd:                                        [  OK  ]
```

## Check NTP status

You can use the **ntpq** command to check the status of NTP synchronization.

```
[root@UplogixControlCenter ~]# ntpq -pc as
```
 
Here's an example that failed because the server doesn't authenticate its packets.

``` 
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 203.0.113.201   .RSTR.          16 u    -   64    0    0.000    0.000 4000.00

ind assID status  conf reach auth condition  last_event cnt
===========================================================
  1 65044  c000   yes   yes   bad    reject
```
 
Here's an example that passes authentication, but just needs a little more
time before it has reliable jitter numbers and will sync the time.

``` 
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 198.51. 100.1   198.51.100.254     6 u   23   64    7    0.378  -8524.2 20934.8

ind assID status  conf reach auth condition  last_event cnt
===========================================================
  1 43013  f014   yes   yes   ok     reject   reachable  1
```

Here, the NTP server passes authentication and is syncing the time.

```
     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
*198.51. 100.1   198.51.100.254     6 u   28   64  377    0.201    0.296   0.068

ind assID status  conf reach auth condition  last_event cnt
===========================================================
  1 56140  f614   yes   yes   ok   sys.peer   reachable  1
```

## Further NTP Authentication troubleshooting

If the output from *ntpq* does not match one of the examples, further troubleshooting may be necessary.

To test ntp auth with ntpdate run the following:

```
[root@UplogixControlCenter ~]# ntpdate -d -a 1 -k /etc/ntp/ntp.keys 203.0.113.201
```
 
To debug a potentially bad configuration file, stop ntpd, and run it in the foreground with the following commands (as root):
 
```
[root@UplogixControlCenter ~]# service ntpd stop
Shutting down ntpd:                                        [  OK  ]

[root@UplogixControlCenter ~]# ntpd -u ntp:ntp -d

ntpd 4.2.6p5@1.2349-o Tue Jan 1 10:09:21 UTC 2016 (1)
22 Jan 02:41:24 ntpd[29666]: proto: precision = 0.067 usec
22 Jan 02:41:24 ntpd[29666]: 0.0.0.0 c01d 0d kern kernel time sync enabled
event at 0 0.0.0.0 c01d 0d kern kernel time sync enabled
Finished Parsing!!
restrict: op 1 addr 0.0.0.0 mask 0.0.0.0 mflags 00000000 flags 000005d0
restrict: op 1 addr :: mask 0.0.0.0 mflags 00000000 flags 000005d0
restrict: op 1 addr :: mask :: mflags 00000000 flags 000005d0
restrict: op 1 addr 127.0.0.1 mask 255.255.255.255 mflags 00000000 flags 00000000
restrict: op 1 addr 198.51.100.60 mask 255.255.255.255 mflags 00000000 flags 00000004
22 Jan 02:41:24 ntpd[29666]: ntp_io: estimated max descriptors: 1024, initial socket boundary: 16
22 Jan 02:41:24 ntpd[29666]: Listen and drop on 0 v4wildcard 0.0.0.0 UDP 123
22 Jan 02:41:24 ntpd[29666]: Listen and drop on 1 v6wildcard :: UDP 123
22 Jan 02:41:24 ntpd[29666]: Listen normally on 2 lo 127.0.0.1 UDP 123

--- output removed ---
```