<!-- 5.4 -->

Interactive command to specify how often the Uplogix Local Manager archives session, alarm, alert and audit data to the Uplogix Control Center, and how many archives are stored locally during an extended inband network outage (up to 100). 

Much of the statistical data the collected by the Uplogix system is device statistics and logs used to make autonomous decisions.  This data is available for export if desired.

The archive process rolls off this information to the server for long-term analysis and reporting. 

# Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
config system archive
```

# Usage 

```
[admin@UplogixLM]# config system archive
--- Existing  Values ---
Time Between Archivals: 3,600
Maximum Archives Stored Locally: 100
Change these? (y/n) [n]: y
--- Enter New Values ---
Time Between Archivals (300-36000 seconds): [3600]:
Maximum Archives Stored Locally (1-100): [100]:
Remove Queued Archive Files: (y/n) [n]:
Do you want to commit these changes? (y/n):
```

To decrease network impact, increase the Time Between Archivals setting, which is given in seconds.

The Remove Queued Archive Files prompt allows you to purge archive files that have not yet been pushed to the Control Center.

# In the Uplogix web interface

**Inventory > group page > System > Archive** - specific to this inventory group

**Inventory > Local Manager page > System > Archive** - specific to this system

# History 

3.4 - This command was introduced

# Related commands 

- **show system archive**
