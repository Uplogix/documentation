<!-- 5.4 -->

Used to pull operating system files from network devices. The files are compared to the versions previously stored. If the content is different, the version stored as current is moved to previous, overwriting the existing previous version, and the new file is stored as current. 

The pull process will retry several times if it does not successfully retrieve the file. The file transfer protocol and number of retries are options that default to the best settings for the device; these can be overridden using the **config settings** command. File transfer may be configured as console, TFTP, FTP or XModem.

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, ND Satcom, Netscreen, Tasman

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
pull os 
```

# Usage 

The OS is scheduled to be pulled periodically during initial configuration. The default interval is 2 weeks. The pull os operation can be removed from the schedule using the config removejob command.

```
[admin@UplogixLM (port1/1)]# pull os
Starting pull of Cisco IOS Image
System image file is "slot0:/c3745-js-mz.123-9a.bin"
Backing up os file: slot0:c3745-js-mz.123-9a.bin
Transferring file ...
Receiving c3745-js-mz.123-9a.bin from 172.28.117.22: !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
TFTP upload of c3745-js-mz.123-9a.bin succeeded.
```

# In the Uplogix web interface

Pull operations are automatically scheduled by the Uplogix Control Center.

#History 
--
#Related commands 

- **push os**
- **copy**
