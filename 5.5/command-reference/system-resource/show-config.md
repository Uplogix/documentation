<!-- 5.4 -->

Displays the Uplogix Local Manager's configuration in XML format. The configuration does not include scheduled jobs, device-specific files, or system IP address. To export this information as an XML file, use the **config backup** command.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show config
```

# Usage 

```
[admin@UplogixLM]# show config
<?xml version="1.0" encoding="UTF-8"?>
<EnvoyConfiguration>
    <version>5.1.1</version>
    <users>
        <user>
            <name>admin</name>
            <password>********</password>
            <alertFrequency>0</alertFrequency>
            <alertEligibility>* * * * *</alertEligibility>
            <timeZone>GMT</timeZone>
            <dst>false</dst>
            <active>true</active>
            <radiusUser>false</radiusUser>
            <emails/>
        </user>
    </users>
    <groups/>
    <roles>
        <role>
            <name>admin</name>
            <permissions>
                <permission>
                    <name>allow assimilate</name>
                </permission>
                <permission>
                    <name>allow autorecovery</name>
                </permission>
                <permission>
---Press 'q' to quit, any other key to continue--- [1/82]
- Output removed -
```

# History 

1.3 - This command was introduced.

# Related commands 

- **config backup**
- **config export**
- **config import**
