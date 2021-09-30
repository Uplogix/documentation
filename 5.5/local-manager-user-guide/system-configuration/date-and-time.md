<!-- 5.5.4 -->

<div class='ucc' />Inventory > Local Manager Summary >Â Network > NTP</div>

In most cases, you will not need to set the date and time. To ensure accurate reporting and to coordinate activities across multiple time zones, Uplogix Local Managers use Coordinated Universal Time (UTC); the time is set at the factory.

If the system is configured to work with an Uplogix Control Center, by default it uses the date and time from the Uplogix Control Center's NTP server.

The date and time settings can be adjusted manually, or the appliance can be configured to use a separate Network Time Protocol (NTP) server.

To set the date and time manually, use the interactive **config date** command. Convert your local time to UTC before changing the time on the Local Manager.

> *Displayed time* is based off the timezone setting specified in the logged-in user's account.

```
[admin@UplogixLM]# show date
Displayed time is 11/12/2019 14:21:43 CST
System time is    11/12/2019 20:21:43 UTC
```

> The date and time cannot be set from the Control Center.

To override time and date settings from the Uplogix Control Center, or to specify an NTP server of your own, use the interactive **config system ntp** command to set the NTP server's IP address and optionally add a secondary server in case the primary server fails. 

```
[admin@UplogixLM]# config system ntp
--- Existing  Values ---
Use NTP: No
Change these? (y/n) [n]: y
--- Enter New Values ---
Use NTP (y/n) [y]: y
Automatically configure NTP (y/n) [y]: n
NTP Primary Server Hostname or IP []: 172.30.105.1
NTP Secondary Server Hostname or IP: 
Do you want to commit these changes? (y/n): y
```

**Automatically configure NTP:** The Local Manager can automatically configure NTP settings if 1) DHCP is enabled and 2) the DHCP server has been configured to return one or multiple NTP server addresses. 

To confirm NTP settings, use the **show system ntp** command.