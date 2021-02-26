<!-- 5.4 -->

Opens an editor that allows you to set name/value pairs for an Uplogix Local Manager. These properties can be used by the Uplogix Control Center to generate detailed reports. To set properties for the devices connected to the system, use the **config properties** command.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system properties
```

Within the editor, properties are defined as **<â€œpropertynameâ€> <â€œvalueâ€>**.

Properties may be deleted using the command **no <â€œpropertynameâ€>**.

Use the **exit** command to quit the editor.

# Usage 

Properties are arbitrary pairs of names and values. Examples: 

- Room 312
- location floor4
- assetID 78652

```
[admin@UplogixLM]# config system properties
[config system properties]# installDate 11/10/06
[config system properties]# exit
[admin@UplogixLM]#
```

# In the Uplogix web interface

**Inventory > Local Manager page > System > Properties** - specific to this system

# History 

3.4 - This command was introduced 

# Related commands 

- **show system properties**
- **config properties**
- **show properties**
