<!-- 5.4 -->

Displays logged LMS sessions including session ID, user ID, source address and login/logout timestamps.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show sessions [userID]
```

Use the optional [userID] parameter to filter the session list by user.

# Usage 

```
[admin@UplogixLM]# show sessions
id         user      ip address        logged in        logged out  
------     -----     -------------     ------------     ------------
524289     admin     172.30.4.225      Apr  3 15:01     
524288     admin     172.30.4.225      Mar 30 15:20     Mar 30 17:54
458758     admin     172.30.4.225      Mar 30 14:32     Mar 30 14:32
458757     admin     172.30.4.225      Mar 25 14:07     Mar 25 17:05
458756     admin     172.30.4.225      Mar 20 12:56     Mar 20 13:34
```

# In the Uplogix web interface

**Inventory > Local Manager page > Session Logs** - specific to this 
system

# History 
--
# Related commands 

- **show session**
- **show who**
