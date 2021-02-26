# Overview
In most cases, you will not need to manually set the date and time. NTP is recommended on both the Local Managers and the Control Center for proper synchronization.

<div class='ucc' />Inventory > Local Manager Summary >Â Network > NTP</div>

# Setting the Date and Time

To set the date and time manually, use the interactive **config date** command. Convert your local time to UTC before changing the time on the Local Manager.

> *Displayed time* is based off the timezone setting specified in the logged-in user's account.

```
[admin@UplogixLM]# show date
Displayed time is 02/12/2020 13:26:24 CST
System time is    02/12/2020 19:26:24 UTC
```

> The date and time cannot be set from the Control Center.

To override time and date settings from the Uplogix Control Center, or to specify an NTP server of your own, use the interactive **config system ntp** command to set the NTP serverâ€™s IP address and optionally add a secondary server in case the primary server fails. 

```
[admin@UplogixLM]# config system ntp
--- Existing  Values ---
Use NTP: Auto
No servers found.
Change these? (y/n) [n]: y
--- Enter New Values ---
Use NTP (y/n/auto) [auto]: y
NTP Primary Server IP: 10.10.10.253
NTP Secondary Server IP: 
Do you want to commit these changes? (y/n): y
```

The Local Manager will test each IP as they are submitted. If the server does not respond, an error message will be presented:

```
NTP Primary Server IP: 132.163.96.5
Primary server '132.163.96.5' invalid: server not responding
```

DNS (configured in **config system ip**) is required if you would like to use hostnames instead of IP addresses. If DNS is not configured, an error message will be presented:

```
NTP Primary Server IP: pool.ntp.org
Unknown Host (probably malformed IP).
```

# Automatically Configuring NTP with Zero Touch Deployment

By default, the Local Manager is configured to use DHCP to get an IP address. If DHCP is enabled, and the DHCP server has been configured to return one or multiple NTP server addresses, the Local Manager can automatically configure itself to use those servers. This setting is designated by *Use NTP: Auto*.

# Viewing NTP Information

To view NTP settings, use the **show system ntp** command.

```
[admin@UplogixLM]# show system ntp
Use NTP: Yes
NTP Primary Server Hostname or IP: 10.10.10.253
```

To view additional NTP information, use the **show system ntp verbose** command.

```
[admin@UplogixLM]# show system ntp verbose
Use NTP: Yes
NTP Primary Server Hostname or IP: 10.10.10.253
NTP Secondary Server Hostname or IP: 

     remote           refid      st t when poll reach   delay   offset  jitter
==============================================================================
 t1.dfa3.gq1.dfa .INIT.          16 u    -   64    0    0.000    0.000   0.000
```