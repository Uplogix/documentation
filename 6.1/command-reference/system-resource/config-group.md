<!-- 5.4 -->

Opens an editor that allows you to create and delete group accounts, add and remove users to group accounts, and alter authority for group accounts.

> **Note:** This command cannot create new groups if the Local Manager is managed by a Uplogix Control Center. In this case, you must use the server's web interface to configure group accounts. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config group [no] <"groupname">
```

Use the **no** modifier to delete the group.

Account names must be unique. For example, if there is a user account called "sysadmin" on the Local Manager, you cannot create a group account called "sysadmin".

# Subcommands 

**description** - information about the group. 255 alphanumeric characters.

**group** - an existing group that is to be included in this group.

**user** - a user to be associated with this group. Users can be added iteratively by repeating this command.

**email [in-band | out-of-band] [terse]** - Specify the email address that will receive administrative messages, optionally distinguishing between in-band and outband email addresses. You can add more than one email address by repeating this command. The terse parameter is an optional setting to send only the subject line, which is useful for pagers. The email subcommand is only used to send group related mail - not alerts.

**system <"role">** - authority for the Uplogix Local Manager from defined roles. Authority is additive and multiple roles can be applied to a user by repeating the command.

**start** - group's MMDDYYYYHHMMSS start time - INACTIVE before.

**expire** - group's MMDDYYYYHHMMSS expiration time - INACTIVE after.

**modem <"role">** - authority for the modem from defined roles. Authority is additive and multiple roles can be applied by repeating the command.

**port{1/1..n/n} <"role">** - authority per port from defined roles. Authority is additive and multiple roles can be applied by repeating the command.

**powercontrol <"role">** - authority for the power controller from defined roles. Authority is additive and multiple roles can be applied by repeating the command.

**show** - display current settings.

**no** - used before optional commands to remove attributes or entries.

**exit** - exit the group editor.

# Usage 

```
[admin@UplogixLM]# config group no southwestOps
Group southwestOps deleted from Local Manager
```
```
[admin@UplogixLM]# config group auditors
Group auditors does not exist. Create (y/n): y
[config group auditors]# description auditors
[config group auditors]# email auditors@xyzco.us.com
[config group auditors]# expire 12312007235959
[config group auditors]# port 1/1 analyst
[config group auditors]# port 1/2 analyst
[config group auditors]# port 1/3 analyst
[config group auditors]# port 1/4 guest
[config group auditors]# exit
```

# In the Uplogix web interface

**Administration > Groups** - universally available

# History 

1.1 - This command was introduced.

4.1 - TACACS ACL removed.

# Related commands 

- **config user**
- **show group**
