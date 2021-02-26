<!-- 5.4 -->

This interactive command clears the export queue. This is valuable if a unit was not able to communicate for an extended period of time and the statistical data is no longer relevant. 

> **Note:** Device Statistics, Alarm and Event logs, and SLV statistics will be deleted

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system clear export
```

# Usage 

```
[admin@UplogixLM]# config sys clear export
Remove Queued Export Files (y/n) [n]: y
Successfully removed queued export files.
```

# History 

4.4 - This command was introduced

# Related commands 

**config system clear archive**
