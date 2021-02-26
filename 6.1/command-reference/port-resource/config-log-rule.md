<!-- 5.4 -->

Initializes the rule logging for a particular port. Once configured, a log will be created that displays the Uplogix systemâ€™s rule processing. Rule logging is automatically disabled when the Local Manager reboots.

This task places a significant drain on resources and should be used only for debugging rule execution.

# Command availability 

CLI resource: port, modem

Device makes: All

Modem: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config log rule <enable | disable>
```

# Usage 

```
[admin@UplogixLM (port1/1)]# config log rule enable
```

# History 

2.0 - This command was introduced.

# Related commands 

- **show log rule**
