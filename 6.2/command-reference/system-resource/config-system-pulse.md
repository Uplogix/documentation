<!-- 5.4 -->

Interactive command to set up pulse server use. The pulse address is a server running the echo port (defaults to TCP port 7) and is used to determine network availability and operation. This command allows you to configure the system to use outband dial-up when the pulse fails.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system pulse
```

# Usage 

Choose a pulse host on a network that defines operational minimum for the connected network devices.

> **Note**: The Cisco IOS TCP small server service before IOS 12.4 cannot be used to respond to echo requests from the Uplogix Local Manager.

If the pulse fails four successive requests, this triggers outband connectivity. After the outband connection is established, the pulse must pass five successive requests to drop outband connectivity. Pulse generates an alarm on its first failure.

```
[admin@UplogixLM]# config system pulse
--- Existing  Values ---
Use Pulse: false
Pulse Server IP 1: 127.0.0.1
Pulse Server Port 1: 7
Pulse Server IP 2: 127.0.0.1
Pulse Server Port 2: 7
Pulse Server IP 3: 127.0.0.1
Pulse Server Port 3: 7
Enable Out-of-Band on Pulse Failure: no
Change these? (y/n) [n]: y
--- Enter New Values ---
Use Pulse (y/n) [n]: y
Pulse IP 1 [127.0.0.1]: 198.51.235.1
Pulse Port 1 [7]:
Pulse IP 2 [127.0.0.1]:
Pulse Port 2 [7]:
Pulse IP 3 [127.0.0.1]:
Pulse Port 3 [7]:
Enable Out-of-Band on Pulse Failure (y/n) [n]: y
Remain Out-of-Band after Pulse Success (y/n) [n]: n
Maximum Time Out-of-Band (minutes; 0 means unlimited) [0]:
Do you want to commit these changes? (y/n): y
```

# In the Uplogix web interface

**Inventory > Local Manager page > Out-of-Band > Pulse** - specific to this system

# History 

3.4 - This command was introduced 

# Related commands 

- **show system pulse**
- **config system management**
- **config ppp**
