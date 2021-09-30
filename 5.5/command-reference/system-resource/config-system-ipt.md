<!-- 5.4 -->

Opens an editor to configure the VoIP IPT listener process. Enabling this feature will make the system answer VOIP calls.

A valid SLV license must be applied to access this command. Licenses are managed on the Uplogix Control Center. 

To set up an IPT test, use the **config slv ipt** command.

# Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: Advanced

# Syntax 

```
config system ipt
```

# Subcommands 

**[no] listen** - enable or disable this feature. 

**payload &lt;harvardmale | harvardfemale | dtmf1â€¦dtmf9 | 1khz | 2khz | 3khz&gt;** - the recorded message to play

**[no] subinterface <#>** - subinterface name to listen on 

**duration <#>** - number of seconds the call should last 

**endpoints <#>** - restricts the number of callers.

**show** 

**[no] allow **

**[no] deny **

**exit** - leave the IPT configuration editor.

# Usage 

```
[admin@UplogixLM]# config system ipt
[config system ipt]# listen
[config system ipt]# show
duration 30
endpoints 10
subinterface VoiceVlan
listen true
payload harvardfemale
```

# In the Uplogix web interface

**Inventory > Local Manager page > Automation > IPT** - specific to this system

# History 

3.4 - This command was introduced to replace config Local Manager ipt.

4.4 - Subinterface parameter added to define SLV routing

# Related commands 

- **config slv ipt**
- **show system ipt**