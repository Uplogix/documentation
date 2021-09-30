<!-- 5.4 -->

Opens an editor that allows you to set name/value pairs for a device on one of the system's ports. These properties can be used by the Uplogix Control Center to generate detailed reports. To set properties for the Uplogix Local Manager, use the **config system properties** command.

# Command availability 

CLI resource: port, modem

Device makes: All

Modem: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config properties
```

Within the editor, properties are defined as **<"propertyname"> <"value">**.

Properties may be deleted using the command **no <"propertyname">**.

Use the **exit** command to quit the editor.

Reserved properties:

- _applet_failover_ip
- _applet_failover_ssh_fingerprint
- _applet_failover_ssh_port
- Enhanced_CommandPrompt: [#>]
- Enhanced_LoginPrompt: login:\s
- Enhanced_LogoutCommand: exit\r
- Enhanced_PasswordPrompt: ssword:\s
- Enhanced_WakeupCommand: \r
- Enhanced_TimeoutSeconds 10
- sshIp
- sshPort 
- sshIpOob 
- sshPortOob

# Usage 

Properties are arbitrary pairs of names and values. 

Examples: 

- Room 312
- location floor4
- rack 6
- assetID 78652


```
[admin@UplogixLM (port1/1)]# config properties
[config properties]# installDate 01/16/07
[config properties]# exit
[admin@UplogixLM (port1/1)]#
```

# In the Uplogix web interface

**Inventory > Local Manager page > port detail > Properties** - specific to this device

# History 

2.2 - This command was introduced.

# Related commands 

- **config system properties**
- **show properties**
- **show system properties**
