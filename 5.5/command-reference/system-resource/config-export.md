<!-- 5.4 -->

Exports the Uplogix Local Managerâ€™s configuration to an external host. Using FTP or SCP, an XML representation of the systemâ€™s configuration can be stored for future imports to other Uplogix Local Managers. The XML file can be retrieved using the **config import** command.

You can use the **show config** command to view the information that will be exported.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config export <scp | ftp> <â€œuser@ipAddress:filenameâ€>
```

# Usage 

```
[admin@UplogixLM]# config export ftp kjones@ 203.0.113.2:UplogixLM.xml
```

# History 

1.1 - This command was introduced.

# Related commands 

- **config import**
- **config update**
- **show config**
