<!-- 5.4 -->

Displays rules that can be applied to monitors that initiate alerting and action.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show rule <â€œrulenameâ€ | *>
```

Specify the name of a rule, or use the * character to show all rules defined on the system.

# Usage 

```
[admin@uplogixLM]# show rule modemLineDisconnected
rule modemLineDisconnected
action alarm MODEM_LINE_DISCONNECTED
conditions
modem.response equals "NO DIALTONE" :2i OR
modem.response equals "NO LINE" :2i OR
modem.response matches "1\.40\s+OK" :2i
exit
exit
```

# In the Uplogix web interface

**Inventory > group page > Automation > Rules** - specific to this inventory group

**Inventory > Local Manager page > Automation > Rules** - specific to this system

# History 

1.1 - This command was introduced.

# Related commands 

- **config rule**
- **show ruleset**
