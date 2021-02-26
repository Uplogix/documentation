<!-- 5.4 -->

Opens an editor to define a set of privileges to apply to users and groups. Roles specify permitted commands.

The industry standard admin, security, analyst, operator, and guest roles are predefined but can be customized with this command, or you can create new roles.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config role [no] <â€œrole nameâ€>
```

Include the no modifier to delete the role.

# Subcommands 

Use the no modifier to remove settings. For example, use **no expire** to define the role to be valid indefinitely, if it previously had an expire date.

**[no] allow &lt;command | ?&gt;** â€“ Specify commands that accounts with this role may execute. You may use as a wildcard character. The command **allow ?** displays a list of allowed commands for this role.


**[no] deny &lt;command | ?&gt;** â€“ Specify commands that accounts with this role may not execute. You may use **&#42;** as a wildcard character. The command **deny ?** displays a list of commands denied to this role. Specifically denied commands are filtered from those specifically allowed. The all keyword is overridden by any specific **allow** or **deny** statement. For example, if you issue the **deny show &#42;** command after allowing the **show user** command, the role allows **show user** but no other **show** commands.

**[no] description <â€œtextâ€>** â€“ Provide information about the role. This is a free text field of 255 characters.

**[no] expire &lt;MMDD&gt;** â€“ month and day of the current year after which the role is no longer valid.

**[no] start &lt;MMDD&gt;** â€“ month and day of the current year that the role becomes valid

# Usage 

Use the ? command after the **allow** and **deny** keywords to display a list of privileges.

A user or group may be given more than one role. The current privileges are evaluated for each execution, and may change authority during a userâ€™s session.

The example below shows a role that starts on January 01 and expires on December 31 of the current year. 

```
[admin@uplogixLM]# config role EastNOC
[config role EastNOC] description East Coast NOC
[config role EastNOC] start 0101
[config role EastNOC] expire 1231
[config role EastNOC] allow show*
[config role EastNOC] deny show user, session 
[config role EastNOC] allow config password, ppp-*
[config role EastNOC] allow export
```

# In the Uplogix web interface

**Administration > Roles** - universally available

**Inventory > group page > Security > Roles** - specific to this inventory group

**Inventory > Local Manager page > Security > Roles** - specific to this system

# History 

1.1 - This command was introduced.

# Related commands 

- **show role**
