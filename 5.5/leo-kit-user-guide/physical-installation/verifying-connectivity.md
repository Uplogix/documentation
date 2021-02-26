Before beginning initialization of Iridium and GPS components, verify that basic connectivity is available.

## Testing Iridium

Log into the Local Manager and navigate to the modem resource. By default, the modem has no configuration. Use the **terminal** command to open a session with the modem. Run **ATZ** and **ATi4**. You should receive OK and Iridium in response.

```
[admin@u5000]# modem
 Iridium
[admin@u5000 (modem)]# t
Press ~[ENTER] to exit
Connecting ...
Console session started.

atz
OK

ati4
IRIDIUM
```

The output of **show serial** will show CTS and DSR as FALSE. This is normal for this system.

## Testing GPS

Navigate to the port that the GPS is connected to. Use the **config serial** command to set the baud rate of this port to 4800 (default for Garmin GPS).

Then, use the **terminal** command to open a session with the GPS receiver. You will not be able to enter any commands, but you should see NMEA traffic coming across the port. If there is no data or if the characters are garbled, try adjusting the baud rate or swap in another cable.

<!-- 5.3 -->