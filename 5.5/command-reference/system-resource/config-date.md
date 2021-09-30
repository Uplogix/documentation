<!-- 5.4 -->

Interactive command to set the date and time on the Uplogix Local Manager. Not used with Uplogix Control Center. Local Managers managed by a Uplogix Control Center use the server heartbeat to set the time unless a separate NTP server is configured. If you prefer to use an NTP server to set date and time, use the **config system ntp** command.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config date
```

# Usage 

To maintain accurate timestamps across time zones, use the current UTC time for this setting and rely on the user's time zone setting for offset. If NTP is configured - for example, if the Local Manager is managed by an Uplogix Control Center, the current configuration shows this.

```
[admin@UplogixLM]# config date
*** NTP is configured. ***
Displayed time is 01/16/2010 22:57:41 UTC
Local Manager time is     01/16/2010 22:57:41 UTC
Change these? (y/n) [n]:
```

# History 

1.3 - The user's time offset is displayed.

3.5 - Command now warns if NTP is configured.

# Related commands 

- **show date**
- **config system ntp**
