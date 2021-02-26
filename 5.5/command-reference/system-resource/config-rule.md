<!-- 5.4 -->

Opens an editor that allows you to create rules to be applied to monitors and to initiate alerting and action. For detailed information about writing and using rules, refer to the Guide to Rules and Monitors.

# Command availability

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config rule [no] <"rulename">
```

Using the no modifier with the config rule command deletes the rule.

# Subcommands 

**no** â€“ used before subcommands to remove attributes or entries.

**conditions** â€“ list of elements evaluated from collected data and evaluated using thresholds to determine if rule is true

**description** â€“ Provide information about the rule. This is a free text field of 255 characters. Use the no modifier to clear an existing description.

**start** â€“ ruleâ€™s MMDDYYYYHHMMSS start time â€“ INACTIVE before

**expire** â€“ ruleâ€™s MMDDYYYYHHMMSS expiration time â€“ INACTIVE after

**show** â€“ display current settings

**action &lt;action name&gt; &lt;parameters&gt;** - may be any of the following:

-   alarm [alarmType] [noalert | -a message | -oid id]
- 	certify
- 	clearCounters
- 	clearServiceModule [-i interfaceName]
- 	clearValue [system | monitor] variable_name
- 	decrementValue [system | monitor] variable_name
- 	emailSystemLog [email address]
- 	event [alarmType] [-a message]
- 	execute [-raw] [-pattern pattern] [-multiline] [-command command] [-timeout timeout] [-setValue [system | monitor] variable_name value]
- 	incrementValue [system | monitor] variable_name
- 	interfaceCycle [-i interfaceName]
- 	interfaceOff [-i interfaceName]
- 	interfaceOn [-i interfaceName]
- 	powerCycle [delay seconds]
- 	powerOff
- 	powerOn
- 	pppOff
- 	pppOn
- 	pullRunningConfig
- 	pullStartupConfig
- 	pullTech
- 	pushOS [candidate | current | previous]
- 	pushRunningConfig [candidate | current | previous]
- 	pushStartupConfig [candidate | current | previous]
- 	reboot
- 	rebootAll
- 	rebootWorking
- 	restartSystem
- 	restore
- 	serviceProcessorPowerCycle
- 	serviceProcessorPowerOff
- 	serviceProcessorPowerOn
- 	setPosition
- 	setValue [system | monitor] variable_name value
- 	writeStatus [a status message]

Actions are executed in the order they are listed in the rule.

**exit** â€“save the rule and exit the rule configuration editor.

# Usage 

```
[admin@UplogixLM]# config rule carrier
[config rule carrier]# show
description Serial Carrier ProblControl Center
action alarm -a "serial carrier problControl Center"
conditions
interface.operationalStatus equals up AND
interface.lineProtocolStatus equals down AND
serviceModule.currentLossOfFrame equals true AND
serviceModule.currentLossOfSignal equals true
exit
exit
```

# In the Uplogix web interface

**Inventory > group page > Automation > Rules** - specific to this inventory group

**Inventory > Local Manager page > Automation > Rules** - specific to this system

# History 

1.1 - This command was introduced.

3.2 - The execute action was added.

3.4 - The emailLocal ManagerLog and restartLocal Manager actions were renamed emailSystemLog and restartSystem, respectively. The serviceProcessorPower actions were added. The certify, restore, and writeStatus actions were added.

# Related commands 

- **config ruleset**
- **config monitors**
- **show rule**