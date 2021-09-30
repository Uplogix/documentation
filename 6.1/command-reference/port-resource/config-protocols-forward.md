<!-- 5.4 -->

Configures the SSH port forwarding settings.

SSH port forwarding enables access to network services running on the dedicated or management IP addresses of a managed device. Multiple users on multiple workstations can use SSH Port Forwarding concurrently.

To use SSH port forwarding, the managed device's management or dedicated IP address must be configured on the Local Manager. This can be configured using **config init** or **config info**.

# Command availability 

CLI resource: port

Uplogix system: All

LMS offerings: All

# Syntax

```
config protocols forward
```

# Usage 

```
[admin@UplogixLM (port1/1)]# config protocols forward

```
#Subcommands

- **[no] management {port} [onconnect] [protocol]** - Enables forwarding to the management IP address and the port specified. The **no** prefix will remove the forward.



Example: To enable traffic forwarding to port 80 on the managed device's management IP address:
```
[admin@UplogixLM (port1/1)]# config protocols forward
[forward]# management 80
```



- **[no] dedicated {port} [onconnect] [protocol]** - Enables forwarding to the dedicated IP address and the port specified. The no prefix will remove the forward.

Example: To enable traffic forwarding to port 80 on the managed device's dedicated IP address: 

```
[admin@UplogixLM (port1/1)]# config protocols forward
[forward]# dedicated 80
```


- **[no] events** - Turns on event logging for traffic forwarding. The **no** prefix will turn off event logging.


- **show** - Displays the current configuration.


- **exit** - Exits the configuration editor.

# Related Commands

- **show protocols forward**
- **forward**



