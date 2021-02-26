<!-- 5.4 -->

Each port resource on the Local Manager comes with its own file system for storing configuration files, OS images, output from Power On Self Tests (POST), and the output from a **show tech** command on a managed device. 

Categories in the file system include:

 - Config â€“ Running
 - Config â€“ Startup
 - OS
 - Post
 - Tech

For each category type, multiple versions can be stored.

* **Candidate**: Used for staging a new configuration or OS prior to update or upgrade
* **Current**: The current version of file running on the managed device
* **Previous**: The previous version running on the managed device before it was replaced by Current
* **Archive #**: Previous versions that were running on the managed device.  The file system will store up to 20 archived versions
* **Named**: user-defined version names. The file system will store up to 5 named configuration versions and 6 named OS versions

The built-in version names will continue to cycle as new running configurations are detected. 

# Viewing files

Use the **show directory -v** command to view the files in the Uplogix file system for a managed device.

```
[admin@UplogixLM (port2/2)]# show dir -v
All times shown in UTC.

Type     Version    Size        Date          Name
-------  ---------  ----------  ------------  ------------
Config
    Running
         current    4112        Nov  4 22:10  running-config
         previous   4095        Oct 15 15:32  running-config
         archive 1  4099        Oct 15 15:30  running-config
         archive 2  4146        Oct  8 20:59  running-config

    Startup
         current    4148        Oct 15 20:59  startup-config
         previous   4152        Oct 15 15:30  startup-config
         vlandata   780         Oct 15 20:59  vlan.dat
         archive 1  4132        Oct  8 20:59  startup-config

OS
         current    70542428    Oct  8 21:00  c2900-universalk9-mz.SPA.151-4.M.bin

Tech
         current    417818      Oct 15 15:22  showTech

Post
         current    4621        Oct 15 15:25  readPost

[admin@UplogixLM (port2/2)]#
```

# User-defined file version names

The user-defined version names feature allows users to assign unique names to files stored in the Uplogix file system for managed devices, and to use those named files for the push, pull, copy, and delete file operations. The named file will remain untouched until it is deleted or overwritten. Up to five configuration files of each type may be named and up to six named OS files may be stored in the local file system. File names are limited to nine characters in length.

There are a few situations where the Local Manager automatically creates a named configuration and OS file. The advanced Cisco IOS driver will back up that VLAN database from a switch and store it as a named startup-config file called *vlandata*. The OS Policy feature will store a standard OS file that is referenced for the given make and model in an OS Policy on the Control Center as a named OS file with the name *standard*.

A user must have a role with the following permissions in order to complete the operations described for this feature:

 - **show directory** â€” Displays stored files on a port resource
 - **copy** â€” Copies a stored file
 - **delete** â€” Deletes a stored file
 
# Copying and Naming Files

Use the **copy** command to rename a file or to move it. The syntax for the copy command is:

```
copy [options] {source} {destination}
Where each parameter is made up of the following choices:
Type = <os | running-config | startup-config | tech | post>
Version = <candidate | current | previous | <user ver> | archive #>
User versions can include A-Z, a-z, 0-9, and _,  1 to 9 characters.
Port = port #/#
```

Example of copying the current running-config to a user-named running-config with the name â€œgoldenâ€:

```
[admin@UplogixLM (port1/3)]# copy running-config current golden
copy succeeded
[admin@UplogixLM (port1/3)]# show directory
Type		Version		Size			Date				Name
-------	----------		------		------------		------------
Config
Running
Current		7592			17 Feb 12:52		running-config
golden		7592			17 Feb 12:51		running-config
```

# Deleting Files

Use the **delete** command to remove a named file from the Uplogix file system.

> Built-in versions (current, previous, archive) cannot be deleted.

The syntax for the **delete** command is:

```
delete <Type> <user-defined version>
```

An example of deleting a named file from the file system:

```
[admin@UplogixLM (port1/3)]# delete running-config golden
Really delete runningConfig, "golden"? (y/n): y
```