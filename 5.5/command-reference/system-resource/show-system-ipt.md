<!-- 5.4 -->

Displays the current SLV IPT Listener settings â€“ if the Uplogix Local Manager is configured to answer SIP calls, this command displays what will be reported. To view IPT tests that have been configured, use the **show slv ipt** command. 

A valid SLV license must be applied to access this command. Licenses are managed on the Uplogix Control Center.

# Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: Advanced

#Syntax 

```
show system ipt
```

# Usage 

**duration** â€“ the length of the recorded message in seconds
**endpoints** â€“ the number of calling numbers permitted.
**listen** â€“ true if IPT Listener is enabled, false if not
**payload** â€“ the test recording selected.

```
[admin@UplogixLM]# show system ipt
duration 30
endpoints 10
listen true
payload harvardfemale
```

# In the Uplogix web interface

**Inventory > Local Manager page > Automation > IPT** - specific to this system

# History 

3.4 - This command was introduced to replace show Local Manager ipt.

# Related commands 

- **config system ipt**
