<!-- 5.4 -->

Displays the Uplogix Local Managerâ€™s settings for data export. To configure export settings, run **config system export**. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

#Syntax 

```
show system export
```

# Usage 

```
[admin@UplogixLM]# show system export
Enable Export: true
Enable While Out-of-Band: true
Time Between Exports (seconds): 3600
Maximum Exports Stored Locally: 100
File Copy Protocol: scp
Destination Hostname or IP: 10.100.2.178
Destination Port: 22
Username: xyzAus01
Password: ********
Directory: LMdata


```

# In the Uplogix web interface

**Inventory > group page > System > Export** - specific to this inventory group

**Inventory > Local Manager page > System > Export** - specific to this system

# Related commands 

- **config system export**