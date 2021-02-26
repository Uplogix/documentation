<!-- 5.4 -->

Displays rules and/or rulesets.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show ruleset <â€œruleset nameâ€ | *>
```

Specify the name of a ruleset, or use the * character to show all rulesets defined on the system.

# Usage 

Rules separated by the pipe | character are evaluated in parallel. Rules separated by commas are evaluated sequentially; evaluation stops at the first match.

```
[admin@uplogixLM]# show ruleset default
ruleset default
description Rules designed to troubleshoot Serial Interfaces
rules
carrier | physical
exit
exit
```
```
[admin@UplogixLM]# show ruleset recoverConsole
ruleset recoverConsole
description recovering the device when it has become unusable
rules
consoleHung, cpuFiveMinuteAverageGreaterThan90, cpuOneMinuteAverageGreaterThan90
exit
exit
```

# In the Uplogix web interface

**Inventory > group page > Automation > rule sets **- specific to this inventory group

**Inventory > Local Manager page > Automation > Rule Sets** - specific to this system

# History 

1.1 - This command was introduced.

# Related commands 

**config rule**
**config ruleset**
**config monitors **
**show rule**
