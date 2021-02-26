<!-- 5.4 -->

Provides a proxied command interface to devices.  Standard transactional configuration management is applied if configured.  

# Command availability 

CLI resource: port

Device makes: Comtech, Sea Tel

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
device execute "<command to execute>" [-d]
```

The <command to execute> must be a valid command.

**-d** <delay>  Delay between repeated execution of the commands.  Delay execution ends with a ctrl-c

# Usage 

```
[admin@UplogixLM (port1/1)]# device execute S â€“d 5
running-config saved to archive as current.
SIA@PL0116 @P
>
SHA@@L0116 @P
>
SHP@PL0116 @P
>
beginning pull of running-config
Pulled 79 configuration lines.
running-config was pulled
running-config saved to archive as current
```

#History 

3.5 - This command was introduced.

# Related commands
--
