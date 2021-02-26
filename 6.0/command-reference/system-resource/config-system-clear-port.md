<!-- 5.4 -->

When you disconnect a device from a port, its configuration information remains stored on the Uplogix Local Manager until it is explicitly cleared. The **config system clear port** command removes a previously configured device from the ports database. 

> **Note:** If you are deleting a virtual port or removing an option card/expansion unit, use the config system clear slot command to clear the hardware from the database before you clear the ports with this command.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system clear port <slot/port>
```

You can use the wildcard character * to clear all ports on the option card. This will clear all possible ports (n/1 through n/16) rather than detecting how the option card is populated.
# Usage 

```
[admin@UplogixLM]# config system clear port 2/3
Clearing port 2/3 will delete all associated data.
Continue? (y/n): y
port2/3 cleared
```

```
[admin@UplogixLM]# config system clear port 1/*
Clearing port 1/* will delete all associated data.
Continue? (y/n): y
port1/1 cleared
port1/2 cleared
port1/3 cleared
port1/4 cleared
port1/5 cleared
port1/6 cleared
port1/7 cleared
port1/8 cleared
port1/9 cleared
port1/10 cleared
port1/11 cleared
port1/12 cleared
port1/13 cleared
port1/14 cleared
port1/15 cleared
port1/16 cleared
```

# History 

3.4 - This command was introduced.

# Related commands 

**config system clear slot**
