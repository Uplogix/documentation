<!-- 5.4 -->

Interactive command to change the CLI session timeout. If not modified, sessions time out after five minutes of inactivity.  This timeout is overridden if the user is connected to an end device in terminal mode with a higher timeout value.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system timeout
```

# Usage 

```
[admin@UplogixLM]# config system timeout
Current session timeout is 5 minutes.
Change these? (y/n) [n]: y
Timeout (5 to 120 minutes): 15
```

# In the Uplogix web interface

**Inventory > group page > System > Timeout** - specific to this inventory group

**Inventory > Local Manager page > System > Timeout** - specific to this system

# History 

3.4 - This command was introduced.

#Related commands 

- **show system timeout**
