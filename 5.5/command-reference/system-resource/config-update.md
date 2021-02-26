<!-- 5.5.3 -->

Updates the Uplogix Local Manager's operating system to another version.

This command copies the file from the remote file system, executes an integrity checksum, migrates the data to the new database, installs it; then restarts the system on the new version.  If the system cannot start after the update, the software version that shipped on the chassis will be loaded.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config update <scp | ftp> <"userId@IPaddress:filename">
```

```
config update http <http://host/fileName>
```

```
config update usb ["filename"]
```

```
config update UCC category/file 
```

> **Note**: the ignoreDataLoss parameter is normally used to upgrade .

# Usage 

```
[admin@UplogixLM]# config update SCP admin@198.51.28.172:lms5.4.bin
Password:*******
Retrieved 'lms5.4.bin' from 198.51.28.172.
```

The usb option is only available when a USB flash drive is connected to the system. The binary file needs to be available from the flash drive.



```
config update usb UplogixOS-5.5.3.34684-genericx86.bin
```

You can also specify files in subfolders this way: 

```
config update usb upgrade_files/UplogixOS-5.5.3.34684-genericx86.bin
```

> **Note**: Uplogix recommends using a 1 GB FAT16 formatted USB flash drive. Upgrading the system from a FAT32 formatted flash drive may keep the Local Manager from restarting after the upgrade.

The update may be retrieved from the Uplogix Control Center using the **config update UCC &lt;category&gt;/&lt;filename&gt;** syntax, if the file has previously been added to the Uplogix Control Center's file archive in the category specified by the command.



# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all system that match the selected filter

**Inventory > Local Manager page > schedule button** - specific to this system

# History 

1.06 - FTP support was added.

3.3 - HTTP and USB flash drive support were added.

3.5 - The Control Center category/file parameter was added.

#Related commands 

--
