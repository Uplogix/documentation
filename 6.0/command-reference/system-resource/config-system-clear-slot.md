<!-- 5.4 -->

This command is used to remove a previously configured virtual slot, expansion module or option card from the database. Port data is retained.

Use this command if you remove an option card from an Uplogix Local Manager.

When removing hardware, you must clear the slot from the database to prevent alarms.

> **Note**: When you remove hardware permanently, use the config system clear port command also, to ensure that the port data is completely cleared from the database.

# Command availability 

CLI resource: system

Uplogix system: All 

LMS offerings: All

# Syntax 

Uplogix 3200 Local Manager: 

```
config system clear slot <1 | 2>
```

Uplogix 5000 Local Manager: 

```
config system clear slot <2 | 3>
```

# Usage 

```
[admin@UplogixLM]# config system clear slot 2
```

> **Note:** Embedded slots cannot be cleared

# History 

3.4 - This command was introduced 

# Related commands 

--