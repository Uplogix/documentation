<!-- 5.4 -->

Resets the deviceâ€™s telco interface and forces renegotiation. Rules can be defined to automate this operation using the *clearServiceModule *action.

# Command availability 

CLI resource: port

Device makes: Cisco

Uplogix system: All

LMS offerings: All

# Syntax 

```
clear service-module <â€œinterface nameâ€>
```

â€œinterface nameâ€ specifies the service module to be cleared.

# Usage 

```
[admin@UplogixLM (port1/1)]# clear service-module Serial0/1
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all devices that match the selected filter
**Inventory > Local Manager page > port detail > schedule button** - specific to this device

# History 

2.0 - This command was introduced.

# Related commands 

--
