<!-- 5.4 -->

Opens an editor that allows you to define banner text to display before or after login.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system banner <login | welcome>
```

#Usage 

The login banner is displayed to users prior to logging in. Some SSH clients do not support displaying a login banner prior to authenticating.

The welcome banner is presented after login. 

Use exit on a line by itself to leave the editor.

```
[admin@UplogixLM]# config system banner login
Type 'exit' on a line by itself to exit
[config system banner login]# unit UplogixLM
[config system banner login]# exit
```

```
[admin@UplogixLM]# config system banner welcome
Type 'exit' on a line by itself to exit
[config system banner welcome]# Successfully logged in to unit UplogixLM
[config system banner welcome]# exit
```

# In the Uplogix web interface

**Inventory > group page > System > Banners** - specific to this inventory group

**Inventory > Local Manager page > System > Banners** - specific to this system

# History 

3.4 - This command was introduced to replace config Local Manager banner.

# Related commands 

- **show system banner**
