<!-- 5.4 -->

Opens an editor that allows you to create, edit, and delete user accounts. 

> **Note:** This command has no functionality if the system is managed by a Uplogix Control Center. In this case, use the Control Centerâ€™s web interface to configure user accounts. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config user [no] <â€œusernameâ€>
```

Account names must be unique. For example, if there is a group account called "sysadmin" on the system, you cannot create a user account called "sysadmin".

# Subcommands 


The wildcard character may be used to apply to many resources (such as ports) at once.

**alert eligible** - availability window for alerting, in cron format - for example, &#42; 23-14 &#42; &#42; 1-5 to specify any minute during the hours from 11:00 p.m. to 2:00 p.m. UTC, any day of the month, any month, Monday through Friday. Alerts will be sent only during the times specified. 

**alert frequency** â€“ maximum alert threshold defining the frequency a user will receive email alerts. Entered in desired number of minutes between alerts

**alert threshold** â€“ number of minutes alarms are present  before alerts are sent.

**show** â€“ display current settings.

**exit** â€“ exit the user editor.

**no** â€“ used before optional commands to remove attributes or entries.

**description** â€“ Information about the user; up to 255 alphanumeric characters.

**disabled** - allows you to suspend the account without deleting it. Use no disabled to reactivate a disabled account.

**start** â€“ accountâ€™s MMDDYYYYHHMMSS start time â€“ INACTIVE before.

**expire** â€“ accountâ€™s MMDDYYYYHHMMSS expiration time â€“ INACTIVE after.

**system <â€œroleâ€>** â€“ authority for the Uplogix Local Manager from defined roles. Authority is additive and multiple roles can be applied to a user. If you do not give the account a role with the "allow login" permission on the system resource, this user will not be able to log in to the LMS command line.

**modem <"role">** - authority for the modem from defined roles. Authority is additive and multiple roles can be applied by repeating the command. If you do not give the account a role on the modem resource, the user will not be able to use any commands to work with the modem.

**port <â€œportnumberâ€> <â€œroleâ€>** â€“ authority per port from defined roles. Authority is additive and multiple roles can be applied. If you do not give the account a role on a given port resource, the user will not have any access to that port.

**powercontrol <â€œroleâ€>** â€“ authority for the power controller from defined roles. Authority is additive and multiple roles can be applied. If you do not give the account a role on the powercontrol resource, the user will not be able to use any commands to interact with the power controller.

**password** â€“ userâ€™s password. The password is stored in an irreversible Sha-1 hashed MD5 encrypted  format . If entered in text, it is converted. If the hashed version is entered (created on the system), it is stored intact and can be typed/pasted into the field.

> **Note**: If another user views your session using the show session command, the config user interaction will be displayed exactly as it appears to you, including any password that you set. In no other case is the password ever displayed in clear text. For security, set or change the password using the config password command after you exit the config user editor. 

> **Note**: Do not create a password that ends with a space character. When you attempt to log in using a password that ends with a space, the Uplogix Local Manager strips the space character and the login fails.

**authorized keys** - SSH certificates may be used instead of passwords. They are also used in place of locally cached passwords if remote authentication  servers are unavailable. Multiple certificates may be added to the authorized keys field of a userâ€™s account, but each must be pasted in a single contiguous line.

**email [in-band | out-of-band] [terse]** â€“ Specify the email address that will receive administrative messages, optionally distinguishing between in-band and out-of-band email addresses. You can add more than one email address by repeating this command. The terse parameter is an optional setting to send only the subject line, which is useful for pagers.

**label &lt;label name&gt; <â€roleâ€>** - â€“ authority per labeled resource from defined roles. Authority is additive and multiple roles can be applied. If you do not give the account a role on a given label resource, the user will not have any access to that resource.

**subscribe** â€“  by port, chassis, or interface. Syntax for this subcommand is **subscribe [system | powercontrol | port <â€œport numberâ€>]  [chassis | interface <â€œinterfacenameâ€>] -w <#>**  to choose the scope and content of alerts. **subscribe** alone will subscribe to all messages. Additional arguments narrow the scope of the subscription to ports, power control, or the system itself; and further arguments focus alerts to a managed deviceâ€™s chassis or particular interface. The final optional **-w** argument is the time to wait before sending alerts on this subscription, expressed in minutes.

**timezone [no dst]** â€“ the time zone offset from UTC for the user, given as +|- 12 UTC. The no dst modifier specifies that time is not to be adjusted for Daylight Saving Time.

# Usage

```
[admin@UplogixLM]# config user adent
[config user adent]# password l3tm31n
[config user adent]# description ISO-OPS Help Desk
[config user adent]# expire 12312007235959
[config user adent]# alert frequency 5
[config user adent]# alert eligible 0 22-08 * * 1-5
[config user adent]# subscribe port 1/1 chassis cpu
[config user adent]# subscribe port 1/1 chassis mem
[config user adent]# subscribe port 1/3 chassis
```

# In the Uplogix web interface

**Administration > Users** - universally available

# History 

1.1 - Added alert eligibility, frequency, email address, time zone offset, alarm subscription, and resource level authorization.

3.2 - Added disabled setting.

4.0 - Removed individual TACACS authorization 

4.5 - Added Label keyword

# Related commands 

- **show user**
