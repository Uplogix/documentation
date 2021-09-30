<!-- 5.4 -->

Displays the permissions associated with a role. Most permissions correspond to LMS commands.

The industry standard admin and guest roles are predefined. The system may also have other roles created using the config role command.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show role ["role name"]
```

show role displays all roles.

# Usage 

```
[admin@UplogixLM]# show role guest
guest
        allow config password
        allow login
        allow ping
        allow show alarms
        allow show date
        allow show directory
        allow show environment
        allow show session
        allow show status
        allow show version
        allow show who
```

# In the Uplogix web interface

Administration > Roles - universally available

**Inventory > group page > Security > Roles** - specific to this inventory group

**Inventory > Local Manager page > Security > Roles** - specific to this system

# History 

1.1 - This command was introduced.

# Related commands 

- **config role**
