<!-- 5.4 -->
The Control Center uses Secure Shell (SSH) v2 software to provide secure remote access. Your remote client application must also support SSH v2. Use the SSH client to initiate a secure remote connection to the server.

> The **root** account is not allowed to log in via SSH. Use the emsadmin account and supplied password.

Supported Secure Shell clients include: 

* PuTTY
* SSH&#8482; Tectia
* VanDyke&#8482; SecureCRT&#8482;
* SSHTerm for Windows
* iTerm for Macintosh OS X
* UNIX's built-in ssh command

For example, from a UNIX command line, type:

```
ssh emsadmin@198.51.100.1
```

> The first time your SSH client connects to an SSH host following installation or upgrade, you may see an SSH key fingerprint message. This is normal. The client usually caches the key for subsequent use and warns if the host has changed, often indicating network eavesdropping.

To ensure security, change the emsadmin password after logging in for the first time. Use the UNIX **passwd** command:

```
[emsadmin@UplogixControlCenter]# passwd
Enter Old Password: ********
New Password [********]: ********
Confirm Password: ********
```

The emsadmin user has super-user privileges with the **sudo** command. Review your security policy to determine if another user account should be created.