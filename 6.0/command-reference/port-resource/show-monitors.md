<!-- 5.4 -->

Displays a list of monitors for the current resource.

# Command availability 

CLI resource: All

Device makes: All

Modem: All

Power controllers: All

Uplogix system: All

LMS offerings: All

# Syntax

```
show monitors
```

# Usage 

```
[admin@UplogixLM (port1/3)]# show monitors
Listing currently scheduled monitors for device: port1/3
1: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor chassis none "" 30
```

# History 

1.1 - This command was introduced.
2.5 - Command now available on modem resource.
3.3 - Command now available on powercontrol resource.

# Related commands 

- **config monitors**
- **config removejob**
