<!-- 5.4 -->

Instructs the managed device to ping another device.

# Command availability 

CLI resource: port

Device makes: Cisco (IOS/NXOS), iDirect, Foundry

Uplogix Local Managers: All

LMS offerings: All

# Syntax

```
device ping <â€œipv4 addressâ€>
```

# Usage

```
[admin@UplogixLM (port1/1)]# device ping 192.168.1.1
pinging 192.168.1.1 failed.
[admin@UplogixLM (port1/1)]# device ping 198.51.235.94
pinging 198.51.235.94 was successful, round trip time was 4
```

# History

2.5.3 - This command was introduced.

# Related commands

- **ping**
