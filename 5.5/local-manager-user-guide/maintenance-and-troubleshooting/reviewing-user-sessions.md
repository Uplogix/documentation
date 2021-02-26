<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary Page > Session Logs</div>

The Local Manager stores the session histories of all users. To view a list of current and previous sessions, use the **show sessions** command.

```
[admin@UplogixLM]# show sessions
Id user ip address logged in logged out
-- ----- -------------- ---------------- -----------
3 dsmith 192.0.2.24 Jul 18 16:58 UTC
2 admin 2001:DB8:3:100::150 Jul 18 12:26 UTC
1 admin 198.51.100.110 Jul 17 12:15 UTC Jul 17 12:25 UTC
```

Use the session id number to view a specific session. The session is displayed page by page.  The **show session** command shows a transcript of what was visible in the CLI window; for example, if the user changed a password using the **config password** command, the password is not displayed.

Type q at any time to quit viewing the display.

```
[admin@UplogixLM]# show session 3
------------------------------------------------------------
User: dsmith
From: 192.0.2.24
Logged In: Dec 18 16:58:54 UTC 2013
Logged Out: Still logged in
------------------------------------------------------------
> Uplogix LMS v5.4 30647 -- Powering Business Uptime
> ------------------------------------------------------------------------------
> Port     Hostname            Status        Con Eth Uptime   Processor   Last 
>                                                            Utilization  Alarm
> ---- ------------------ ------------------ --- --- ------- ----------- -------
>  1/1 AUS-CORE2          OK                  *   *  4d 15m     00/00/01 4d 28m 
>  1/2                                        *   -                             
>  1/3                                            -                             
>  1/4 Sentry3_521ff1     OK                  *   -  4d 34m     0.4 Amps        
>  1/5                                                                          
>  1/6                                                                          
>  MDM embedded                                                                 
>  SYS UplogixLM          OK                      *  4d 1h      11/11/12 26s    
> ------------------------------------------------------------------------------
> Con(sole) or Eth(ernet) link status indicated with '*'
> Processor Utilization displayed as last collected, 1 and 5 minute averages
> Last Alarm displays time since last Alarm matched.
>                   d=day, h=hour, m=minute, s=second
> 
> Ports 1/1-1/4 have dedicated Ethernet.
> Active alarms exist. Email notification is suspended while you are logged in.
> 
> [super@UplogixLM]# port 1/1
> AUS-CORE2 cisco 2610 IOS 12.2(26)
>           Cisco Router
> 
> [super@UplogixLM (port1/1)]# terminal forward
> 
> Press ~[ENTER] to exit.
> 
> 
> Connecting ...
> 
> 
> 
> Console session forwarded.  Press ~[ENTER] to exit.
> 
> 
> AUS-CORE2#
> 
> You have been idle for 150 seconds. Your session will end in 150 seconds.
> 
------------------------------------------------------------
--DONEâ€”
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