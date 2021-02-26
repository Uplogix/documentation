<!-- 5.4 -->

Displays the restrictions placed on automated procedures. Automated procedures may be restricted to occur only at specific times (such as weekends) or at specified minimum intervals (such as no more than every half-hour, or 1800 seconds).

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show restrict <â€œactionNameâ€ | all> [â€œportâ€]
```

# Usage 

```
[admin@UplogixLM]# show restrict reboot
name reboot
port port1/4
mask * * * * 0,6
interval is not defined
```

# History 

1.1 - This command was introduced.

# Related commands 

- **config restrict**
