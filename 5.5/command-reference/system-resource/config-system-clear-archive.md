<!-- 5.4 -->

When a Local Manager is not able to archive for an extended period of time up to 100 archives are queued up to be sent to the Control Center.   If the operator does not want to maintain the data or it is too old to be of use it may be deleted.  

> **Note**: Configuration, Logging, Session and alarm data will be deleted.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system clear archive
```

# Usage 

```
[admin@UplogixLM]# config system clear archive
Remove Queued Archive Files (y/n) [n]: y
Successfully removed queued archive files.	
```

#History 

4.1 - This command was introduced.
