<!-- 5.4 -->

Displays the interactive session log collected during a CLI session with the Uplogix Local Manager. All information originally displayed on the screen is captured. Each user session is logged and the full transcript can be displayed for review. Defaults to the current session if no session number is supplied. The session numbers available can be listed using the **show sessions** command. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show session ["sessionID"]
```
"sessionID" identifies the session to display. 

# Usage 

```
[admin@UplogixLM]# show session 32771
User: pamarvin
From: 198.51.5.24
Logged In: Jul 28 21:31:59 UTC 2017
Logged Out: Jul 28 21:38:10 UTC 2017
------------------------------------------------------------
> Uplogix LMS v5.4.3  -- Powering Business Uptime
> 
> ------------------------------------------------------------------------------
> Port     Hostname            Status        Con Eth Uptime   Processor   Last
>                                                            Utilization  Alarm
> ---- ------------------ ------------------ --- --- ------- ----------- -------
>  1/1 cisco2950          OK                  *      12d 17h  24/29/23

(output removed)
> 
> [admin@UplogixLM]# port 1/1
>  Cisco
>  cisco2950
>
> [admin@UplogixLM (port1/1)]# sho proto sha
> Enable: false
> Using Local Manager management IP: 198.51.151.109
> Port: 0
> 
(output removed)
>
> [admin@UplogixLM]# logo
------------------------------------------------------------
--DONE--
```

# In the Uplogix web interface

**Inventory > Local Manager page > Session Logs** - specific to this system

# History 
--

- **Related commands **
- **show sessions**
