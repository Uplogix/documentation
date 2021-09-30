<!-- 5.4 -->

Orders rules or rulesets to apply to monitors.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config ruleset [no] <"ruleset name">
```

Using the no modifier with the config ruleset command deletes the rule set.

# Subcommands 

**description** - Provide information about the rule set. This is a free text field of 255 characters.

**show** - Display the rule set's current settings.

**rules** - A list of rules applied either in series or in parallel. Rules separated by the pipe | character are evaluated in parallel. Rules separated by commas are evaluated sequentially; evaluation stops at the first match.

**exit** - Save the rule and exit the ruleset editor.

# Usage 

Example 1:

```
[admin@UplogixLM]# config ruleset interfaceDefault
description Default Ethernet Ruleset
rules
lossOfSignalIncrements | lossOfFrameIncrements | aisAlarmIncrements | remoteAlarmIncrements | currentLineCodeViolationsIncrements | currentPathCodeViolationsIncrements | currentFrameLossSecondsIncrements | currentLineErrorSecondsIncrements | currentErroredSecondsIncrements | operationalStatusDown | lineProtocolStatusDown | loadGreaterThan90 | reliabilityLessThan90 | dataCarrierDetectIsDown | dataSetReadyIsDown | dataTerminalReadyIsDown | requestToSendIsDown | clearToSendIsDown | outputQueueDropsRate | intputQueueDropsRate | intputRuntsRate | intputGiantsRate | inputThrottlesRate | inputCrcErrorsRate | inputFrameErrorsIncrements | inputOverrunErrorsIncrements | outputLateCollisionsIncrements | inputIgnoredPacketsIncrements | inputAbortedPacketsIncrements | outputCollisionsRate | outputInterfaceResetsIncrements | outputDeferredIncrements | outputNoCarrierIncrements | outputCarrierTransitionsIncrements
```
Example 2:

```
[config ruleset rulesetOne]# rule1, rule2 |rule 3, rule 4
```

Rule 1 will be evaluated, and if it does not match, rule 2 and rule 3 will both be evaluated. If neither rule 2 or 3 match, rule 4 is evaluated.

# In the Uplogix web interface

**Inventory > group page > Automation > Rule Sets** - specific to this inventory group

**Inventory > Local Manager page > Automation > Rule Sets** - specific to this system

# History 

1.1 - This command was introduced.

# Related commands 

- **config rule**
- **config monitors** 

