<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary Page > Session Logs</div>

The Local Manager stores the session histories of all users. To view a list of current and previous sessions, use the **show sessions** command.

```
[admin@UplogixLM]# show sessions
id         user      ip address        logged in        logged out  
------     -----     -------------     ------------     ------------
425984     admin     172.30.4.225      Mar 10 14:47     
393218     admin     172.30.24.149     Mar  7 13:50     Mar  7 13:50
393217     admin     172.30.4.225      Mar  6 15:55     Mar  6 17:56
393216     admin     172.30.4.225      Mar  5 13:59     Mar  5 14:39
```

Use the session id number to view a specific session. The session is displayed page by page.  The **show session** command shows a transcript of what was visible in the CLI window; for example, if the user changed a password using the **config password** command, the password is not displayed.

Type q at any time to quit viewing the display.

```
[admin@UplogixLM]# show session 294926
------------------------------------------------------------
User: super
From: 172.30.105.40
Logged In: Feb 28 19:34:29 GMT 2020
Logged Out: Feb 28 19:40:40 GMT 2020
------------------------------------------------------------
> Permission granted for pass-through
> Session started through direct ssh pass-through to port1/1
> Press ~[ENTER] to exit.
> 
> 
> Connecting ...
> 
> 
> Logging out of device...
> 
> Console session started.  Press ~[ENTER] to exit.
> 
> AUS-CORE con0 is now available
```

If the Local Manager is managed by a Control Center, user sessions can be viewed through the Uplogix web interface: Inventory > Local Manager page > Session Logs

###Port Buffer Log

In some cases you may wish to review the contents of a port buffer. Navigate to the desired port and use the show buffer command.
Syntax:
```
show buffer [-raw | -previous]
```

The command show buffer displays the most recent 1 MB of data. Use the optional -previous parameter to view the "previous" buffer.

Use the optional -raw parameter to display the buffer contents without additional formatting.

You may wish to redirect the command output to a file using the pipe character.

###Outband Log

The Local Manager logs detailed dialer, PPP, IP, and VPN setup and teardown information when it attempts to bring up an out-of-band connection (either in the event of an in-band network failure or during an out-of-band network test via the ppp cycle command). This information can be very helpful when troubleshooting out-of-band network configuration or infrastructure issues.  Use the show log outband command on the Local Manager to view the log for the last successful or failed attempt to communicate out-of-band.

###Embedded Modem Troubleshooting

You can issue the pull tech command followed by the show tech command at the modem resource to display information about the modem that can be helpful when troubleshooting modem problems. This command collects information about line voltage and loop current for V.92 modems as well as network registration state, signal strength and modem functionality mode for cellular modems.

<!-- 5.2 -->