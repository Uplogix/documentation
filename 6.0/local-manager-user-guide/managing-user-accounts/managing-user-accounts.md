# Overview

If the Local Manager is not managed by a Control Center, the **config user** and **config group** commands allow you to create accounts unique to that Local Manager.

If the Local Manager is managed by a Control Center, the Control Center web interface must be used for the tasks in this section. The **config user** and **config group** commands cannot be used when the Local Manager is under management.

The **show user** and **show group** commands present account details for individual user accounts and groups, respectively.

# Viewing user account details

The **show user** command returns user account details. To view a single user account, specify the username. You can view all user accounts with the **show user** <strong>*</strong> command.

```
[admin@UplogixLM]# show user ajones
ajones
created 07/15/2011 16:41:34 UTC
password ********
alert eligible * * * * *
timezone US/Central dst
email ajones@xyzco.com
powercontrol - admin
modem - admin
system - admin
port1/1 - guest
port1/2 - guest
port1/3 - guest
port1/4 - guest
subscribe powercontrol
subscribe modem
subscribe system
subscribe port 1/1
subscribe port 1/2
subscribe port 1/3
subscribe port 1/4
```

<div class='ucc' />Administration > Users</div>

# Viewing groups

To display all groups, use the **show group** command.  To view a specific group, use **show group [groupname]**.

```
[admin@UplogixLM]# show group southwestOps
southwestOps
created 07/10/2007 18:01:16 UTC
description southwest region ajoness
email southwest_ops@xyzco
start 20-07-15 00:00:00.0
expire 2009-12-31 23:59:59.0
Group is currently INACTIVE
user  amarvin
user  ajones
user  lprosser
user  fchurch
powercontrol - guest
modem - guest
system - guest
port1/1 - guest
port1/2 - guest
port1/3 - guest
port1/4 - guest
```

<div class='ucc' />Administration > Groups</div>

# Creating and editing user accounts

The **config user** command opens an editor that allows you to create and edit user accounts. Information in the userâ€™s account may include password, account start and end dates, permissions, alert subscriptions and allowable times to receive alerts, and email address for receiving alerts.
 
To edit a user account, use the **config user [username]** command. If the specified username does not exist, the Local Manager prompts you to create it.

User and group names must be unique. For example, if there is a group account called *sysadmin* on the Local Manager, you cannot create a user account called *sysadmin*.

In the examples in this section, we create and configure a user account called *ajones*.

```
[admin@UplogixLM]# config user ajones
User ajones does not exist. Create (y/n): y
[config user djones]#
```

> Usernames are case-sensitive.

Type **?** to see a list of configurable settings. Type **show** to view the userâ€™s current settings.

``` 
[config user ajones]# ?
Allowable arguments are:
show
alert eligible <cron string>
alert frequency <minutes>
alert threshold <occurrences>
[no] all <role name>
[no] authorized keys
[no] description <description>
[no] disabled
[no] email <email address>
[no] expire <MMddyyyyHHmmss>
[no] label <label name> <role name>
[no] modem <role name>
[no] password <password>
[no] port #/# <role name>
[no] port <hostname> <role name>
[no] port * <role name>
[no] powercontrol <role name>
[no] start <MMddyyyyHHmmss>
[no] subscribe <resource> [chassis] [interface <name>] [-w <minutes>]
[no] system <role name>
[no] timezone <UTC offset> [no dst]
or 'exit' to quit config mode

```

## Password

To log in, users need either passwords or SSH certificates. You can set a password within the **config user** editor with the **password** subcommand:

    [config user ajones]# password pass02

Passwords are case-sensitive.
 
 <div class='warning'>If another user views your session using the **show session** command, the **config user** interaction will be displayed exactly as it appears to you, including any password that you set. In no other case is the password ever displayed in clear text. For security purposes, set or change the password using the **config password** command after you exit the **config user** editor.</div>

Users can change their own passwords with the **config password** command. 
 
 <div class='warning'>Do not create a password that ends with the space character. When you attempt to log in using a password that ends with a space, the Local Manager strips the space character and the login fails.</div>

## Authorized keys

SSH keys may be used instead of passwords. They are also used in place of locally cached passwords if remote authentication servers are unavailable.

Multiple certificates may be added to the authorized keys field of a userâ€™s account, but each must be pasted in a single contiguous line.

```
[config user ajones]# authorized keys 
Each key must be on its own line. Type 'exit' on a line by itself to exit
[config user ajones authorized keys]# ssh-rsa AAAAB3NzaC1yc2EAAAABI-OUTPUT-REMOVED-baCacLjMCxMZpMxE7mQUM= ajones
[config user ajones authorized keys]# 
[config user ajones authorized keys]# exit
[config user ajones]#
```
 
Both RSA and DSA certificates can be used.

Certificate format varies widely among SSH clients. Each vendorâ€™s documentation should be consulted to determine which key formats and encryption algorithms are available.

## Disabled

To suspend a user's account without deleting the account information, use the **disabled** subcommand. For more information on disabling and reactivating accounts, refer to Disabling a user's account and Reactivating a disabled account for more information.

## Alert eligibility and frequency

The eligibility setting is used to restrict alert messages to specified times. The Local Manager determines who will receive alert emails based on the eligibility setting as well as frequency and subscription settings. The setting uses a CRON formatted string. For example, this command:

    [config user ajones]# alert eligible 0 22-08 * * 1-5

would send alert emails to user ajones between 10:00 p.m. UTC to 8:00 a.m. UTC, Monday through Friday.

When the Local Manager has an alert email to send, it will check the alert frequency settings of eligible users. If the user has been alerted within the time set as the alert frequency, the message will not be sent. This setting represents a time frame in which the Local Manager will not send more than one alert.

For example, to limit alerts to no more than one every 10 minutes, use the alert frequency subcommand:

    [config user ajones]# alert frequency 10

## Time zone

Time and date reporting can be customized for each user. The **timezone** subcommand takes a single argument that represents the userâ€™s time offset from UTC. The additional parameter **no dst** can be added if the userâ€™s location does not observe daylight savings time.

    [config user ajones]# timezone -6

## Email

To receive alert messages, a user must have a valid email address set.

    [config user ajones]# email ajones@xyzco.com

You can set more than one email address and you can specify when the Local Manager uses an address â€” only when the Local Manager is operating in-band or only when it is out-of-band.  If you do not specify in-band or out-of-band, the Local Manager uses the address in both situations.

```
[config user ajones]# email ajones@xyzco.com in-band
[config user ajones]# email alerts@xyzco.com out-of-band
```

For more information about alerting, refer to Configuring an account to receive alerts.

## Description

You can set a description for the user by using the **description** subcommand.

    [config user ajones]# description A. Jones- Network Analyst

## Roles and resources
By default, users have no privileges on any resource. Privileges are defined by roles, which are tables of permitted commands. Privileges are granted by assigning appropriate roles on the desired resources to define what the user can do on each resource.

The **config user** command allows user privileges to be customized. The first argument is the resource, followed by a role. The **no** modifier can precede the command to remove privileges.

```
[config user ajones]# system guest
[config user ajones]# port 1/1 guest
[config user ajones]# port 1/2 admin
[config user ajones]# port 1/3 guest
[config user ajones]# no port 1/4 
[config user ajones]# modem guest
```

The admin role (separate from the admin user account) has access to every available command except the **config reinstall** command that is used to factory reset the Local Manager. To manage the Local Manager, at least one user account must be assigned the admin role unless the Local Manager is being managed by a Control Center.

For more information about using roles, refer to Assigning roles.

## Subscriptions
An alert is an alarm that is emailed to subscribed users. Subscriptions allow you to direct alerts to the appropriate personnel.

To receive alerts, users must subscribe to resources they are interested in. To receive all alerts from the Local Manager, use the **subscribe all** command. Users can subscribe to individual resources as well as interfaces on managed devices.

```
[config user ajones]# subscribe port 1/1
[config user ajones]# subscribe system
[config user ajones]# subscribe port 1/3 chassis
[config user ajones]# subscribe port 1/4 interface Serial0/0
[config user ajones]# subscribe port 1/4 interface Serial0/1
```

For more information about alerting, refer to Configuring an account to receive alerts.

## Start and expire dates

By default, user accounts are valid indefinitely; however, they can be set up to begin and end at predefined dates and times. The **start** and **expire** subcommands are used to define the date range. Accounts are active only during the defined period. The account must be active for the user to log in or execute commands. The Local Manager can be configured to send an alert to the user when the account expires.

The start and expire commands take date and time as an argument in MMDDYYYYHHMMSS format.

```
[config user ajones]# start 06212012000000
[config user ajones]# expire 12312014235959
```

This example activates the account on June 21, 2012. The account expires at the end of 2014. Note that start and expire dates use UTC time; if this user is in the Central time zone in the USA, the account will expire at 6 p.m. local time on December 31, 2014.

Start and expire settings can be removed with the no modifier.

```
[config user ajones]# no start
[config user ajones]# no expire
```

## Review a user account after making changes

To verify a user accountâ€™s configuration, use the **show** subcommand while in the user editor. For this example, we have set this user's role to analyst on all resources.

```
[config user ajones]# show
ajones
created 06/18/2013 22:17:52 UTC
description A. Jones- Network analyst
start 06/21/2013 00:00:00 UTC
User is currently INACTIVE
password ***********************
alert frequency 10m
alert eligible 0 22-08 * * 1-5
timezone US/Central dst
email ajones@xyzco.com
modem - analyst
system - analyst
port1/1 - analyst
port1/2 - analyst
port1/3 - analyst
port1/4 - analyst
subscribe powercontrol
subscribe modem
subscribe system
[output removed]
```

# Creating and editing group accounts

Groups are made up of a combination of applied roles, users, and effective times. They can be used to manage authority for a number of users at the same time.

> If the Local Manager is managed by a Control Center, group accounts cannot be managed locally. 

To create a group, use the interactive **config group [groupname]** command. This opens an editor that allows set up of the group's attributes.

```
[admin@UplogixLM]# config group AustinNOC
Group AustinNOC does not exist. Create (y/n): y
[config group AustinNOC]# ?
Allowable arguments are:
show
[no] description
[no] email
[no] system
[no] expire
[no] group
[no] modem
[no] port #/#
[no] start
[no] subscribe
[no] user or 'exit' to quit config mode
```

Account names must be unique. For example, if there is a user account called *sysadmin* on the Local Manager, you cannot create a group account called *sysadmin*.

## Description

To set a description for the group, use the **description** subcommand.

    [config group AustinNOC]# description The NOC Group in Austin

## Email

To set a group email address, use the **email** subcommand.

    [config group AustinNOC]# email AustinNOC@xyzco.com

## Roles and resources

By default, groups have no privileges on any resource. Privileges are defined by roles, which are tables of permitted commands. Privileges are granted by assigning appropriate roles on the desired resources to define what the group can do on each resource. Users in a group inherit the groupâ€™s assigned privileges.

The **config group** command allows group privileges to be customized. The first argument is the resource, followed by a role. The no modifier can precede the command to remove privileges.

```
[config group AustinNOC]# port 1/1 guest
[config group AustinNOC]# no port 1/4 guest
[config group AustinNOC]# port 1/2 guest
[config group AustinNOC]# port 1/2 admin
[config group AustinNOC]# system admin
```
   
For more information about using roles, refer to Assigning roles.

## Start and expire dates

Group accounts may have effective dates, just like user accounts. The start and expire subcommands take date and time as an argument in MMDDYYYYHHMMSS format.

```
[config group AustinNOC]# start 01012012000000
[config group AustinNOC]# expire 12312013235959
```

Start and expire settings can be removed with the **no** modifier.

```
[config group AustinNOC]# no start
[config group AustinNOC]# no expire
```

## Adding and removing users

To add users to a group, use the **user [username]** subcommand.

    [config group AustinNOC]# user dsmith

To remove users from a group, use the **no** modifier with the **user [username]** subcommand.

    [config group AustinNOC]# no user dsmith

# Configuring an account to receive alerts

An alert is an alarm that is emailed to subscribed users. To receive alerts:

* The Local Manager must be configured to use a mail server, refer to Setting originating email address and SMTP server for alerts.
* You must have a user account.
* Your user account must include at least one email address.
* You must be subscribed to the alerts you wish to receive.

Use the **config user** editor to define subscriptions using the **subscribe** subcommand. This allows you to direct alerts to the appropriate personnel.

To subscribe a user to alerts from all resources, use the **subscribe all** subcommand.

In the following example, D. Smith will receive all alerts.

    [config user dsmith]# subscribe all

In the following example, D. Smith will receive alerts from port 1/2, the port 1/3 chassis, the power controller, and the Local Manager.

```
[config user dsmith]# subscribe port 1/2
[config user dsmith]# subscribe port 1/3 chassis
[config user dsmith]# subscribe system
```

D. Smith may choose to limit alerts to specific interfaces that are being monitored on a managed device as follows:

```
[config user dsmith]# subscribe port 1/4 interface Serial0/0
[config user dsmith]# subscribe port 1/4 interface Serial0/1
```

The account can be configured to receive alerts at separate email addresses during in-band and out-of-band operation. Use the **config user** command to set the user's email addresses with either the in-band or out-of-band parameter:

```
[config user dsmith]# email dsmith@xyzco.com in-band
[config user dsmith]# email alerts@xyzco.com out-of-band
```

Setting up different in-band and out-of-band email addresses provides an indication of whether the Local Manager is operating out-of-band, and can allow you to receive alerts through a different email account if your work email account is unavailable because of a network outage.

<div class='info'>The Local Manager does not email alerts if a session is in progress. If alarms occur, they are only emailed after all users have logged out or their sessions have timed out.</div>

The Local Manager aggregates alarms and sends alerts by SMTP-based email every two minutes during an outage. Data from each alarm is included in CSV format.

Although you do not receive alerts while you are logged into the Local Manager, alarms continue to be logged on the Local Manager and to stream to a syslog server if one is configured. If the Local Manager is managed by a Control Center, alarms continue to be updated there as well.

If you log out while there are current alarms, the Local Manager displays the current alarms and prompts you whether to delay alerts or restart them immediately. You may specify a time to delay alerts in hours or minutes. The delay may be up to two hours.

If the Local Manager is managed by a Control Center, you can set up subscriptions to alerts through the Uplogix web interface: *Administration > Users > {User Name} > Alert Subscriptions*

# Disabling a user's account

To disable a user's account without deleting it, open the user account editor with the **config user **command. The subcommand **disabled** preserves the account information while rejecting attempts to log in with that user's credentials.

```
[admin@UplogixLM]# config user ajones
[config user ajones]# disabled
[config user ajones]# exit
```

To verify that the account has been suspended, execute the **show user** command:

```
[admin@UplogixLM]# show user ajones
ajones
created 06/15/2007 16:41:34 UTC
User is currently INACTIVE
password *********************
alert eligible * * * * *
timezone US/Central dst
email ajones@company.com
[Output removed]
```

The account is shown as INACTIVE.

# Reactivating a disabled account

To reactivate an account that has been disabled, open the user account editor with the **config user **command. The subcommand **no** **disabled** reactivates the account. However, the user account is still subject to its start and expire dates.

```
[admin@UplogixLM]# config user ajones
[config user ajones]# no disabled
[config user ajones]# exit
```

The **show user** command lets you verify that the account is no longer inactive.

```
[admin@UplogixLM]# show user ajones
ajones
created 06/15/2007 16:41:34 UTC
password *******************
alert eligible * * * * *
timezone US/Central dst
email ajones@company.com
```
# Deleting an account

When you remove an account, all the account information is deleted. An alternative for user accounts is to disable the account, which allows you to prevent access while preserving the account information.

To delete user account information, use the no modifier with the **config user** command.

    [admin@UplogixLM]# config user no ksmith

To delete a group, use the no modifier with the **config group** command.

```
[admin@UplogixLM]# config group no DallasNOC  
Group DallasNOC deleted
```