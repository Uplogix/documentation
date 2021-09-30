<!-- 5.4 -->

Displays the current welcome and login banners - lines of text displayed before and immediately after login, respectively.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

#Syntax 

```
show system banner
```

#Usage 

```
[admin@UplogixLM]# show system banner
Welcome Banner:
Successfully logged in to unit uplogixLM

Login Banner:
No login banner set.
```

# In the Uplogix web interface

**Inventory > group page > System > Banners** - specific to this inventory group

**Inventory > Local Manager page > System > Banners** - specific to this system

# History 

3.4 - This command was introduced to replace show Local Manager banner.
3.5 - Command feedback specifies when no banner is configured.

# Related commands 

- **config system banner** 
