<!-- 5.4 -->

The Uplogix Local Manager employs a AAA system for user management:

- Authentication
- Authorization
- Auditing

For a user to be able to log into an appliance, they must satisfy the following requirements:

- The user account exists
- The user authenticates correctly (password or authorized SSH key)
- The user has authorization to access a resource (system, ports, and/or modem)

Auditing requirements will be met automatically by the system through session logging.

# Minimum Requirements to Log In

In this example, we will configure the minimum requirements for user Brad Smith to log into the Local Manager.

```
[admin@UplogixLM]# config user bsmith
User bsmith does not exist. Create (y/n): y
[config user bsmith]# password affable
[config user bsmith]# system guest
[config user bsmith]# exit
```

When Brad Smith tries to log in, he will be presented with:

```
$ ssh 172.30.151.111
bsmith's password: ********
Uplogix LMS v5.4 30647 -- Powering Business Uptime
------------------------------------------------------------------------------
Port     Hostname            Status        Con Eth Uptime   Processor   Last 
                                                           Utilization  Alarm
---- ------------------ ------------------ --- --- ------- ----------- -------
 SYS UplogixLM          OK                      *  1d 2h      14/13/12 20s    
------------------------------------------------------------------------------
Con(sole) or Eth(ernet) link status indicated with '*'
Processor Utilization displayed as last collected, 1 and 5 minute averages
Last Alarm displays time since last Alarm matched.
 d=day, h=hour, m=minute, s=second
Active alarms exist. Email notification is suspended while you are logged in.
[bsmith@UplogixLM]#
```

Note that Brad Smith's dashboard is limited to the resources on which he has privileges.

**Both authentication and authorization requirements must be met before a user can log in.**
