<!-- 5.4 -->

Interactive command that restarts the Uplogix Local Manager. Use the **reboot** command to restart devices connected to the system.

Rules can be defined to automate this operation using the restartSystem action.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
restart
```

# Usage 

This will end your session. Restart usually takes 90 seconds. 

```
[admin@UplogixLM]# restart
Are you sure you want to restart? (y/n): y
Restarting Local Manager...
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all system that match the selected filter

**Inventory > Local Manager page > schedule** - specific to this system

# History 

--

# Related commands 

- **reboot **
- **shutdown**
