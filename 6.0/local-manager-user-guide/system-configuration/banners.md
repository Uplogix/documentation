# Overview

Uplogix Local Managers can display two banners:

* welcome banner - displayed after successful authentication.
* login banner - displayed prior to login.

By default, no banners are defined.

<div class='ucc' />Inventory > Local Manager Summary > System > Banners</div>

# Setting Banners

You can define banners to display any required legal information or operational notes with the **config system banner** editor command. The **login** parameter allows you to edit the banner that is displayed before login. The **welcome** parameter allows you to edit the banner that is displayed after login. Enter the desired text, which may use more than one line. When you are finished, use the **exit** command to leave the editor and return to the main CLI.

LMS Version **5.5** and above supports replacement tokens in the banner for build information:

- **${version}** - Version number
- **${build}** - Build label
- **${bname}** - Build name
- **${hb}** - Heartbeat version



```
[admin@UplogixLM]# config system banner welcome
Type 'exit' on a line by itself to exit.
[config system banner welcome]# Welcome to Uplogix LM ${version}!
[config system banner welcome]# exit
```

On login, a user will see:

```
uplogix-user@linux-server:~$ ssh admin@10.10.1.108
admin@10.10.1.108's password: 
Welcome to Uplogix LM 6.0!
```

<div class='warning' />Do not use non-printing characters in banners. Spaces are considered printing characters.</div>

> Some SSH clients do not support the login banner.

You can verify the current banners with the **show system banner** command:

```
[admin@UplogixLM]# show system banner
Welcome Banner:
Welcome to Uplogix LM ${version}!

Login Banner:
No login banner set.
```

In the above example, no login banner has been configured.

# Clearing Banners

To clear a banner, use the **config system banner** command with either the **login** or the **welcome** parameter. Type **exit** without entering any other text.
 
Use the **show system banner** command to verify that you have cleared the banner.

```
[admin@UplogixLM]# config system banner welcome
Type 'exit' on a line by itself to exit
[config system banner welcome]# exit

[admin@UplogixLM]# show system banner
Welcome Banner:

Login Banner:
No login banner set.
```

Banners can also be configured from the Uplogix Control Center under Inventory > Local Manager Summary > System > Banners.