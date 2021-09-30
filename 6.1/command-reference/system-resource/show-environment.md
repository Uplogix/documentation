<!-- 5.4 -->

Displays the current and average temperature and (if applicable) humidity recorded by the Uplogix Local Manager.

# Command availability 

CLI resource: system

Uplogix system: 400, 3200

LMS offerings: All

#Syntax 

```
show environment
```

# Usage 

The Uplogix 3200 Local Manager is available with an optional external 1-Wire&#8482; temperature sensor. Older 4-port Uplogix Local Managers use an internal temperature sensor mounted at the air intake. The information returned by this command depends on which sensor (if any) is installed.

```
[admin@UplogixLM]# show environment
Current temperature: 84.83 degrees F
Current humidity:    25.81%
Average temperature over the last hour: 84.56 degrees F
Average humidity over the last hour:    25.33%
Power supply status: Power 2 inactive
Primary Ethernet status:   Link up
Secondary Ethernet status: Link down ; interface down
Tertiary Ethernet status:  Link down

```

# In the Uplogix web interface

**Inventory > Local Manager page > System > Environment** - current environmental data for this system

# History 
--

#Related commands 

- **config environment**
