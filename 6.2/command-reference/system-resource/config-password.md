# Overview
This command can be used to change the password of a local account. If the Local manager is managed by a UCC, this command is disabled.
# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config password ["username"]

```

# Usage

If you use the command **config password** without including a username, this allows you to change your own password. The **config password "username"** command allows you to change the password for the specified user account without supplying the current password. You must have the appropriate privileges to change another user's password.

```
[admin@UplogixLM]# config password
Old Password:********
New Password [********]: ********
Confirm Password: ********
Password changed.

[admin@UplogixLM]# config password djones
New Password: ********
Confirm Password: ********
Password changed.
```

If the LM is managed by a Control Center, an error message will be displayed.

```
[admin@UplogixLM]# config password
Users may not be edited when the system is managed.
```

> **Note**: Do not create a password that ends with a space character. When you attempt to log in using a password that ends with a space, the Uplogix Local Manager strips the space character and the login fails.

# In the Uplogix Control Center

**Administration > Users** - universally available

# History 

--

# Related commands 

--
