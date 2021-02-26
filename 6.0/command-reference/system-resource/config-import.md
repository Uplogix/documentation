<!-- 5.4 -->

Imports an XML representation of the Uplogix Local Managerâ€™s configuration from an external host or USB connected drive. This merges with the configuration currently stored on the Local Manager. Some elements cannot be imported and are ignored. Importing of users is ignored when the Local Manager is managed by a UCC.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
[admin@UplogixLM]# config import
usage: import <method> <target>
methods: ems, ftp, scp, http, https, usb

Import via management server
ex. config import ems <category>/<fileName>
Import via FTP or SCP
ex. config import ftp <userId@host:fileName>
ex. config import scp <userId@host:fileName>
Import via HTTP or HTTPS
ex. config import http://host-or-ip/file.xml
ex. config import https://server/file.xml
Import via USB
ex. config import usb <fileName>
```

# Usage 

```
[admin@UplogixLM]# config import FTP kjones@192.0.2.33:xyzcoAus01.xml
```

This command imports the XML document produced with the **config export** command.

Validation is performed on all fields before the imported values are committed. The imported configuration will be automatically rolled back if the import is unsuccessful.

Changes to a portâ€™s information will require the port to be reinitialized. The values will be present but must be individually accepted to assure proper communication with the device. Previously uninitialized ports do not require initialization since the new information is not replacing any current values..

The file may be imported from the Uplogix Control Center using the **config import ems 	<category>/<filename>** syntax, if the file has previously been added to the Uplogix Control Center's file archive in the category specified by the command.

# History 

1.1 - This command was introduced.

3.5 - Added Control Center category/file parameter.

4.4 â€“ Added USB

# Related commands 

- **config export**
- **show config**
