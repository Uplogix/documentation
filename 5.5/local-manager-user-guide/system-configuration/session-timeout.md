<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary >Â System > Timeout</div>

Local Managers disconnect users after a specified number of minutes of inactivity. The default timeout is five minutes. Use the **config system timeout** command to change this interval.

```
[admin@UplogixLM]# config system timeout
Current session timeout is 5 minutes.
Change these? (y/n) [n]: y
Timeout (5 to 120 minutes): [5]: 120
```

This example changes the inactivity timeout to 120 minutes.

> This setting does not change the terminal pass-through timeout, which is a separate feature handled in **config settings** on a port resource.