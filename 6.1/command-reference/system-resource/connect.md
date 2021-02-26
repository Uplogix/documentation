<!-- 5.4 -->

Connect to another Uplogix Local Manager via SSH. This command cannot connect the system to any other host, and it cannot be used to connect to more than one other Uplogix Local Manager at a time.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
connect [â€œuser@â€] <â€œip/ipv6 addressâ€> [â€œportâ€]
```

# Usage 

If you omit the username, your current login will be used.

When you log out, you are returned to the session from which you connected.

```
[admin@UplogixLM]# connect 198.51.238.103
Connecting to 198.51.238.103
admin's password: ********
Uplogix LMS v5.4 -- Powering Business Uptime

------------------------------------------------------------------------------
Port     Hostname            Status        Con Eth Uptime   Processor   Last
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
 1/1 tasman6300         OK                  *
 1/2 Solaris Build Box                       *      262d 23             118d 20

- Output removed -

------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
                  d=day, h=hour, m=minute, s=second

[admin@UplogixLM2]#
```

# History 

1.4 - This command was introduced.

# Related commands 

--
