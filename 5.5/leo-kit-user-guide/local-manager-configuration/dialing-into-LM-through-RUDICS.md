<!-- 5.5 -->

The following steps allow you to dial into Local Managers through an Iridium modem without the UCC GUI.

## Connect to RUDICS

### Method 1: Telnet directly into RUDICS via PuTTY:


Open PuTTY to display the configuration window. Enter the IP address of the RUDICS server and select 'Telnet' as the connection type. The port number should be provided to you by Iridium.


![Putty - IP and Tunnels](http://uplogix.com/support/docs/img/putty-rudics-telnet4.jpg)

Once you have successfully connected, you should be able to issue modem commands.

### Method 2: Telnet to RUDICS via the UCC command line.


SSh to the UCC

```
login as: emsadmin
emsadmin@UplogixUCC's password:
Last login: Mon Jun 18 16:20:28 2018 from 192.34.24.11
[emsadmin@UplogixUCC ~]$
```
Telnet to the RUDICS router by issuing the command **telnet [rudicsIP] [port]**  
 
```
[emsadmin@UplogixUCC ~]# telnet 172.30.123.98 2663

Entering character mode
Escape character is '^]'.
```
## Prepare the session by setting the serial settings
 
Once you are connected to RUDICS, issue the commands **ATZ**, **ats29=8**, and **ats57=9660**, allowing the modem to return 'OK.'
 
```
ATZ
OK
ats29=8
OK
ats57=9660
OK

```

## Dial into the Local Manager
The dial command is **atdi** and the phone number with no spaces.
```
atdi00881693144440
```

