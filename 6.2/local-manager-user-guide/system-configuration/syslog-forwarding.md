<div class='ucc' />Inventory > Local Manager Summary > Network > Syslog</div>

The interactive command **config system syslog** allows you to enable syslog forwarding.

Specify the server IP address and port number, and select the syslog facility to write to (such as local1, local2, etc).

```
[admin@UplogixLM]# config system syslog
--- Existing  Values ---
Syslog enabled: no
Syslog server IP: 
Syslog port number: 514
Syslog facility: 
Change these? (y/n) [n]: y
--- Enter New Values ---
Enable syslog? (y/n) [n]: y
Syslog server IP: 192.168.1.253
Syslog port number [514]: 
Syslog facility: local5
Do you want to commit these changes? (y/n): y
```