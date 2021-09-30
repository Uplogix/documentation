<!-- 5.4 -->

Imports an XML representation of the Uplogix Local Manager's configuration from an external host or USB connected drive. This merges with the configuration currently stored on the Local Manager. Some elements cannot be imported and are ignored. Importing of users is ignored when the Local Manager is managed by a UCC.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config import < scp | ftp > userId@IP:filename
config import ems <category>/<filename>
config import usb  [filename]
```

# Usage 

```
[admin@UplogixLM]# config import FTP kjones@ 192.0.2.33:xyzcoAus01.xml
```

This command imports the XML document produced with the **config export** command.

Validation is performed on all fields before the imported values are committed. The imported configuration will be automatically rolled back if the import is unsuccessful.

Changes to a port's information will require the port to be reinitialized. The values will be present but must be individually accepted to assure proper communication with the device. Previously uninitialized ports do not require initialization since the new information is not replacing any current values..

The file may be imported from the Uplogix Control Center using the **config import ems 	&lt;category&gt;/&lt;filename&gt;** syntax, if the file has previously been added to the Uplogix Control Center's file archive in the category specified by the command.

# History 

1.1 - This command was introduced.

3.5 - Added Control Center category/file parameter.

4.4 - Added USB

# Related commands 

- **config export**
- **show config**
