This command exports the Uplogix Local Managerâ€™s configuration to an external host. Using FTP or SCP, an XML representation of the systemâ€™s configuration can be stored for future imports to other Uplogix Local Managers. The XML file can be retrieved using the **config import** command.

You can use the **show config** command to view the information that will be exported.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
usage: export <method> <target>
methods: ftp, scp, usb

Export via FTP or SCP
ex. config export ftp <userId@host:fileName>
ex. config export scp <userId@host:fileName>

Export via USB
ex. config export usb <fileName>
```

# Usage 

```
[admin@UplogixLM]# config export scp uplogixlm@10.10.10.2:UplogixLM83X.xml
Password: *******
File successfully sent to 10.10.10.2.
```

# History 

1.1 - This command was introduced.
5.x - USB added as export target

# Related commands 

- **config import**
- **config update**
- **show config**
