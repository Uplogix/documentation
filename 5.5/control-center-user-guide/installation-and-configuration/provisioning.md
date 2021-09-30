<!-- 5.4 -->
Configure the Control Center using one of these methods:

* Connect a standard VGA monitor, a keyboard and a mouse
* Configure using the console port by connecting your computer directly to the server using the DB-9 connector on the server's rear panel. Supported terminal clients include: Windows HyperTerminal, ZTerm (Macintosh OS X), Minicom (Unix/Linux)

> Console default communication settings are 9600 baud, 8 data bits, 1 stop bit, no parity, and no flow control. Set your terminal emulator to use ANSI encoding for best results.

Log into the Control Center using the **emsadmin** user account. The default password is **password**. To run the initial setup, use the **netSetup.sh** script located in /uplogix/embassy/.

> If you make a typo while inputting information, use CTRL-U to clear the line.

```
[emsadmin@UplogixControlCenter ~]$ /uplogix/embassy/netSetup.sh 
Run Setup? (y/n) [y] y
Install multi application servers? (y/n) [n] n
Interface eth0 IP Address: 192.0.2.11
Interface eth0 Gateway: 198.0.2.1
Interface eth0 Netmask: 255.255.255.0 
Interface eth0 IPv6 mode? (none/static/autoconf) [none]         
Note: Echo (pulse) will be enabled on eth1 if the eth1 interface is configured.
Configure eth1? (y/n) [n] y
Interface eth1 IP Address: 192.0.2.12
Interface eth1 Gateway: 198.0.2.1
Interface eth1 Netmask: 255.255.255.0
Interface eth1 IPv6 mode? (none/static/autoconf) [none]             
** Warning: You must reboot after configuring hostname. **
Configure hostname? (y/n) [n] y
Hostname[UplogixControlCenter]: DocumentationUCC
Configure DNS? (y/n) [n] y
Primary DNS Server IP: 198.51.100.1
Secondary DNS Server IP: 198.51.100.2
Tertiary DNS Server IP: 
Configure NTP? (y/n) [n] y
Primary NTP Server IP: 198.51.100.112
Secondary NTP Server IP: 
Change emsadmin password? (y/n) [n] 
Commit? (y/n) y
```

After committing your changes, the server displays messages as it updates the affected files. Once it's complete, you should see this message displayed:

```
-----------------------------------------------------
When you are ready, run 'ucc chkconfigon' and reboot.
-----------------------------------------------------
```
Become root and run the command **ucc chkconfigon**. This command configures services to start up automatically on boot. If it is not run, you will need to manually start services using the "ucc start" command as root after each reboot.
```
[emsadmin@UplogixControlCenter ~]$ sudo su -
[sudo] password for emsadmin:
[root@UplogixControlCenter ~]# ucc chkconfigon
[root@UplogixControlCenter ~]# 
```      

After that is run, reboot when you are returned to the command line prompt.