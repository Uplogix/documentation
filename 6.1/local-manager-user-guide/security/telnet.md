<div class='ucc'>Inventory > Local Manager (or Group) Summary page > Network > Protocols</div>

By default, the Local Manager allows users to connect via SSH to TCP port 22 only. The Local Manager can be configured to also allow Telnet connections.

To allow the Local Manager to respond to Telnet requests on TCP port 23, use the **config system protocols telnet enable** command.

```
[admin@UplogixLM]# config system protocols telnet enable
Telnet will be enabled after the next system restart.
```

> This command takes effect after you restart the Local Manager.
