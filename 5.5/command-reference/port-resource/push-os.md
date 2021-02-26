<!-- 5.4 -->

Used to push operating system files to network devices. Use **config settings** to set the primary and secondary file transfer protocols and the maximum number of attempts.  TFTP, FTP, and XModem are supported. Named OS files referenced in the command line are case sensitive.
 
Rules can be defined to automate this operation using the pushOs action.  

# Command availability

CLI resource: port

Device makes: Alcatel, Cisco, Juniper, ND Satcom, Netscreen, Tasman

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
push os <candidate | current | previous | named>
```

# Usage 

```
[admin@UplogixLM (port1/1)]# push os candidate
System image file is "flash:/c1700-y-mz.123-9.bin"
3 interfaces and 3 types found.
Information logged Before Upgrade
Serial Number: FOC08060NSX
Make : cisco
Model : 1760
OS Type : IOS
OS Version : 12.3(9)
Uptime : 14 hours, 22 minutes
Device Image Verified.
Sending c1700-y-mz.123-1a.bin to 10.10.10.1: !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
TFTP download of c1700-y-mz.123-1a.bin succeeded.
Retrieving running-config from device ...
Complete. running-config pulled.
Retrieving running-config from device ...
Complete. running-config pulled.
Issuing 'reload'
98304C1700 platform with 65536 Kbytes of main memory
decompressing
Image decompressed
Image decompressing
Image decompressed
Device loaded
Post complete.
Serial Number: FOC08060NSX
Make : cisco
Model : 1760
OS Type : IOS
OS Version : 12.3(1a)
Uptime : 0 minutes
3 interfaces and 3 types found.
Push OS succeeded.
```

The push os operation will try the secondary transfer method if the primary method fails, and will make up to the specified number of attempts if necessary. 

The push os operation can be scheduled to automatically update using the **config schedule** command.

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > Local Manager page > port detail > schedule** - specific to this system

# History 

4.3 Named OS files added

#Related commands 

- **pull os**
- **copy**
