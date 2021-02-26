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
id        user        ip address      logged in            logged out
-----     -------     -----------     ----------------     ----------------
14        admin       198.51.5.24     Jul 29 16:49 UTC
13        admin       198.51.5.24     Jul 29 14:53 UTC     Jul 29 15:23 UTC
12        admin       198.51.5.24     Jul 28 23:45 UTC     Jul 28 23:52 UTC
11        admin       198.51.5.24     Jul 28 22:44 UTC     Jul 28 23:36 UTC
10        admin       198.51.5.24     Jul 28 21:37 UTC     Jul 28 22:16 UTC
9         pamarvin    198.51.5.24     Jul 28 21:31 UTC     Jul 28 21:38 UTC
8         admin       198.51.5.24     Jul 28 21:17 UTC     Jul 28 21:36 UTC
7         admin       198.51.5.24     Jul 28 16:08 UTC     Jul 28 17:20 UTC
6         admin       198.51.5.24     Jul 25 23:49 UTC     Jul 25 23:55 UTC
5         admin       198.51.5.24     Jul 25 23:13 UTC     Jul 25 23:43 UTC
4         admin       198.51.5.24     Jul 25 19:24 UTC     Jul 25 22:31 UTC
3         admin       198.51.5.24     Jul 25 16:46 UTC     Jul 25 18:26 UTC
2         admin       198.51.5.24     Jul 25 15:30 UTC     Jul 25 16:45 UTC
1         admin       198.51.5.24     Jul 25 15:24 UTC     Jul 25 15:29 UTC
```

# In the Uplogix web interface

**Inventory > Local Manager page > Session Logs** - specific to this 
system

# History 
--
# Related commands 

- **show session**
- **show who**
