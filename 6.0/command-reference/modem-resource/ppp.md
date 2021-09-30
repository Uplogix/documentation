<!-- 5.4 -->

Establishes or ends outband dial-up management connectivity. When you know you will be making device changes that will compromise the integrity of your SSH connection, this functionality will establish a consistent communications link used to monitor or alter the network changes.

Rules can be defined to automate this operation using the pppOn and pppOff actions.

If the cycle keyword is used, the additional parameter for duration or heartbeat must be added to define what determines a successful cycle.  If heartbeat, the command will return successful if the full heartbeat completes.  If duration, the connection is maintained for the duration specified and then disconnected.

# Command availability 

CLI resource: modem

Modem: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
ppp <on | off | cycle [duration [minutes] | heartbeat [number of full heartbeats] >
```

# Usage 

```
[admin@UplogixLM (modem)]# ppp on
PPP Local Address is 4.230.144.126
PPP is turned on
```

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all equipment that matches the selected filter

**Inventory > Local Manager page > Schedule button** - specific to this system

# History 

2.5 - This command was introduced.

4.2 - Cycle keyword added

# Related commands 

- **config ppp**
- **show ppp**
