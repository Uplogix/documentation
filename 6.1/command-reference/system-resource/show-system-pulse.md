<!-- 5.4 -->

Displays the Uplogix Local Managerâ€™s pulse settings. Pulse determines network connectivity by sending packets to an echo host. The system brings up the dial-up outband network if the pulse fails.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
show system pulse
```

# Usage 

```
[admin@UplogixLM]# show system pulse
Use Pulse: false
Pulse Server IP 1: 172.16.200.103
Pulse Server Port 1: 7
Pulse Server IP 2: 127.0.0.1
Pulse Server Port 2: 7
Pulse Server IP 3: 127.0.0.1
Pulse Server Port 3: 7
Enable Out-of-Band on Pulse Failure: yes

```

# In the Uplogix web interface

**Inventory > Local Manager > Out-of-Band > Pulse** - specific to this system

# History 

3.4 - This command was introduced to replace show envoy pulse.

#Related commands 

- **config system pulse**
