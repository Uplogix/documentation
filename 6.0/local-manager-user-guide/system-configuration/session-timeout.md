<div class='ucc' />Inventory > Local Manager Summary >Â System > Timeout</div>

By default, Local Managers are configured to automatically log out an idle user after 5 minutes. To modify this timeout, use the **config system timeout** command.

```
[admin@UplogixLM]# config system timeout
Current session timeout is 5 minutes.
Change these? (y/n) [n]: y
Timeout (5 to 120 minutes) [5]: 120
```

When the idle timeout expires, the user will be presented with a message and disconnected.

```
[admin@UplogixLM]# 
You have been idle for 300 seconds, your SSH session is ending.
Connection to 10.10.10.24 closed.
```

> This setting does not change the terminal pass-through timeout, which is a separate feature handled in **config settings** on a port resource.