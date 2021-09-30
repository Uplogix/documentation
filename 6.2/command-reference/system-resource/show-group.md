<!-- 5.4 -->

Displays group accounts and individual group account attributes.

# Command availability 

CLI resource: system

Uplogix system : All

LMS offerings: All

# Syntax 

```
show group [groupname]
```

Use the [groupname] parameter to show information about a specific group account, or omit it to show a list of group accounts.

# Usage 

```
[admin@uplogixLM]# show group southwestOps
southwestOps
created 06/15/2007 18:01:16 UTC
description southwest region operators
email southwest_ops@xyzco.us.com
start 2020-07-01 00:00:00.0
expire 2020-12-31 23:59:59.0
Group is currently INACTIVE
user  amarvin
user  adent
user  lprosser
user  fchurch
powercontrol - operator
modem - operator
system - operator
port1/1 - operator
port1/2 - operator
port1/3 - operator
port1/4 - operator
```

# In the Uplogix web interface

**Administration > Groups**

# History 

3.2 - Added account creation timestamp.

# Related commands 

- **config group**
