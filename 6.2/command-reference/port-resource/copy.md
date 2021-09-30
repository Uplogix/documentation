<!-- 5.4 -->

Move files between ports and to/from the Uplogix Local Manager from a remote file system.

# Command availability 
CLI resource: port

Device makes: 3Com, Alcatel, Cisco, Comtech EF Data, Garmin, HP, iDirect, Juniper, ND Satcom, Netscreen, Nortel, Sun, Tasman, TippingPoint, native, server

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
copy <"source"> <"destination">
```
Copy from one port to another port:  

```
copy <["port"]<"type"> <"version">> <["port"] <"version">>
```

Port is assumed to be this port if not specified.

Copy from this port to remote host:  

```
copy <<"type"> <"version">> <scp | ftp> <"userName@IP[:file]">
copy <"type"> <"version"> Control Center category/file
```

Copy from remote host to this port:  

```
copy <<scp | ftp> <"userName@IP:file">> <<"type"> <"version">>
copy Control Center <category/file> <"type"> <"version">
```

"source" and "destination" parameters are made up of the following choices:

- **type** = <os | running-config | startup-config | tech | post>
- **version** = <candidate | current | previous | <user ver> | archive #>
User versions can include A-Z, a-z, 0-9, and _,  1 to 9 characters.
- **port** = port #
            
# Usage 
Only file types relevant to the device type are supported and are placed in the device's file system on the Uplogix system.

```
[admin@UplogixLM (port1/1)]# copy os current port 1/2 candidate
[admin@UplogixLM (port1/1)]# copy port 1/2 os current previous
[admin@UplogixLM (port1/1)]# copy running-config current SCP joeuser@198.51.235.93
password: ********
Sending... File successfully sent to 198.51.235.93.
```
```
[admin@UplogixLM (port1/1)]# copy FTP joeuser@198.51.235.95:running-config running-config
Retrieved 'running-config' from 198.51.235.9 
```

In the example below, the running-config file for the device on port 1/1 is copied to the file archive on the Local Manager Management Station.

```
[admin@UplogixLM (port1/1)]# copy running-config current Control Center configs/Aus01-router.cfg     
 
File successfully sent to 198.51.161.252. 
copy succeeded
```

# History 

1.07 - This command was introduced.

1.4 - Ability to copy tech, post, and archive files added.

3.4 - Added Control Center category/file as a source/destination.

# Related commands 
--
