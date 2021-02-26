<!-- 5.4 -->

This command displays results from the rules engine as it evaluates conditions. 

Before you can show the rule log, you must enable rule logging with the **config log rule** command.

# Command availability 

CLI resource: system, port, modem

Device makes: All

Modem: All

Uplogix system : All

LMS offerings: All

# Syntax 

```
show log rule [-c] [-i <â€œinterfaceâ€>] [-m <â€œemailâ€>] [-n <#>] [-r <â€œruleâ€>]
```
**-c** - Show only chassis rule events.
**-i <â€œinterfaceâ€>** - Show only rule events for a particular interface.
**-m <â€œemailâ€>** - Email address to send the report.
**-n <#>** - Maximum number of messages to show.
**-r <â€œruleâ€> **- Show only rule events for the specified rule.

# Usage 

```
[admin@UplogixLM (port1/1)]# show log rule -n 25 -r consoleHung
```
# History 
--

# Related commands 

- **config log rule**
