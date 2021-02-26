<!-- 5.4 -->

Interactive command to configure the auxiliary Ethernet port.  Configuration defaults to bonded (Layer2).  Choices for the secondary Ethernet include bonded, capture and outband.

Bonded selection will fail over within milliseconds.  Fail back will require 30 seconds.

If the selection is capture, the switchport should be configured as a port mirror directed to a specific VLAN or Ethernet port to be analyzed.

Outband will enable the interface when outband operations are proceeding, and bring the interface down when they are suspended.
 
# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system secondary
```

# Usage 

```
[admin@UplogixLM]# config system secondary
--- Existing  Values ---
Type: bonded
Bonding Link: yes
Primary Ethernet Link: yes (bonded active)
Auxiliary Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values ---
Type [bonded]: capture
speed/duplex [auto]:
Warning: Remote connections may be lost if you commit changes.
Do you want to commit these changes? (y/n):

```

# In the Uplogix web interface

**Inventory > group page > Network > Secondary Ethernet** - specific to this inventory group

**Inventory > Local Manager page > Network > Secondary Ethernet** - specific to this system

# History 

4.2 - This command was introduced

4.3 â€“ Capture option added 

# Related commands 

- **show system secondary**
- **config system bonding**
- **show system bonding **
