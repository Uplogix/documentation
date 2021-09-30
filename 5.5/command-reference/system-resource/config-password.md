<!-- 5.4 -->

Interactive command for changing account passwords. This allows an administrator to reset a user's password without knowing the previous password. If a Local Manager is managed by a UCC, this functionality is disabled for all but the admin user.

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
[admin@UplogixLM]# config password tmcmillan
New Password: ********
Confirm Password: ********
Password changed.
```

> **Note**: Do not create a password that ends with a space character. When you attempt to log in using a password that ends with a space, the Uplogix Local Manager strips the space character and the login fails.

# In the Uplogix web interface

**Administration > Users** - universally available

# History 

--

# Related commands 

--
