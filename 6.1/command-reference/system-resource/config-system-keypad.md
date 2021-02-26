<!-- 5.4 -->

Enables or disables the keypad on the front panel of an Uplogix Local Manager. This change does not prevent users from shutting down or restarting the system from the keypad. By default, the keypad is enabled.

# Command availability 

CLI resource: system

Uplogix system: 5000, 3200

LMS offerings: All

# Syntax 

```
config system keypad <enable | disable>
```

#Usage 

```
[admin@UplogixLM]# config system key disable
Keypad Configuration: disabled
[admin@UplogixLM]# config system key enable
Keypad Configuration: enabled
```

# In the Uplogix web interface

**Inventory > group page > System > LCD** - specific to this inventory group

**Inventory > Local Manager page > System > LCD** - specific to this system

# History 

3.4 - This command was introduced to replace config Local Manager keypad.

# Related commands 

- **show system keypad**
