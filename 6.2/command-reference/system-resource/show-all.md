<!-- 5.4 -->

Display console, authentication, make, model, OS configuration, current utilization, and memory statistics. If you use this command from the system resource, the information will be returned for all other resources. If you use this command from a port resource, information for all ports will be displayed.

# Command availability 

CLI resource: All

Device makes: All

Modem: All

Power controllers: All

Uplogix system: All

LMS offerings: All

# Syntax 
```
show all
```

# Usage 

```
[admin@UplogixLM]# show all
Collecting device information . . .
--- port1/1 ---
Hostname: tasman-6300-ds3
Description: tasman6300
Make: tasman
Model: 6300
OS: TiOS
OS Version: r6
Management IP:
Current CPU Utilization: 0%
CPU Utilization (1 minute average): 0%
CPU Utilization (5 minute average): 0%
Total Memory: 268435456 bytes
Used Memory: 55705024 bytes
Free Memory: 177453792 bytes
console user: tasman
console password: ********
enable user:
enable password: ********
Serial Bit Rate: 9,600
Serial Data Bit: 8
Serial Parity: none
Serial Stop Bit: 1
Serial Flow Control: none
Null modem: false
DSR: false
CTS: false
RX : 6,806,757
TX : 249,371
Overrun Errors: 0
--- port1/2 ---
- Output removed -
```

You may wish to redirect the output of this command to a file. See Redirecting command output to a file on page 26..

# History 

1.2 - Added serial information.

# Related commands 

- **show status**
- **show dashboard**
