<!-- 5.4 -->

Displays the interactive session log collected during a CLI session with the Uplogix Local Manager. All information originally displayed on the screen is captured. Each user session is logged and the full transcript can be displayed for review. Defaults to the current session if no session number is supplied. The session numbers available can be listed using the **show sessions** command. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show session [â€œsessionIDâ€]
```
â€œsessionIDâ€ identifies the session to display. 

# Usage 

```
[admin@UplogixLM]# show session 524288
------------------------------------------------------------
User: admin
From: 172.30.4.225
Logged In: Mar 30 15:20:00 GMT 2020
Logged Out: Mar 30 17:54:37 GMT 2020
------------------------------------------------------------
> You have accessed an Uplogix Local Manager.
> 
> Uplogix LMS v6.0 35800 -- Powering Business Uptime

(output removed)

> [admin@UplogixLM]# config system secondary
> --- Existing  Values ---
> Type: bonded
> Bonding Link: yes
> [E1] Primary Ethernet Link: yes (bonded active)
> [E2] Auxiliary Ethernet Link: no (bonded)
> [E3] Internal SFP Ethernet Link: no (bonded)
> Change these? (y/n) [n]: y
> --- Enter New Values ---
> Type [bonded]: capture
> speed/duplex [auto]: 
> Warning: Remote connections may be lost if you commit changes.
> Do you want to commit these changes? (y/n): y
> 
```

# In the Uplogix web interface

**Inventory > Local Manager page > Session Logs** - specific to this system

# History 
--

- **Related commands **
- **show sessions**
