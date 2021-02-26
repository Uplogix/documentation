# Overview 
<div class='ucc' />Inventory > Local Manager (or Group) Summary Page > Network > Protocols</div>

Terminal pass-through is available on the port and modem resources and is enabled on a device-by-device basis. This feature allows an SSH session to be opened directly to the device, passing through the Local Manager, while retaining the Local Managerâ€™s rollback capabilities, session logging, and authorization checking.

To configure terminal pass-through, navigate to the desired resource and use the **config protocols pass-through** command to specify either SSH or Telnet and optionally, the TCP port number. Command syntax is:

```
config protocols pass-through <enable | disable> <telnet | ssh> [â€œport numberâ€]

[admin@UplogixLM (port1/1)]# config protocols pass-through enable ssh
Pass-through port will be 2101.
SSH port change will take place after the next system restart.
```

By default, device ports map to TCP ports starting at 2001. Alternate TCP ports (1023 â€“ 9999) may be specified if desired.

> This setting takes effect after you restart the Local Manager.

Once configured, instead of logging in to the Local Manager, navigating to the port, and issuing the **terminal** command, you can open an SSH session directly to the device using the pass-through port number assigned.

```
xyzcouser@central:~$ ssh -p 2101 admin@198.51.100.254
admin@198.51.100.254's password: *******
Permission granted for pass-through
Press ~[ENTER] to exit
```