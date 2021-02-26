<!-- 5.4 -->

When you disconnect a device from a port, the Local Manager retains the device's configuration data. You can clear this data and return the port to its factory default configuration using the command **config system clear port** from the system resource.

```
[admin@UplogixLM]# port 2/1
 tasman 6300 tios
 tasman
[admin@UplogixLM] (port2/1)]# exit
[admin@UplogixLM]# config system clear port 2/1
Clearing port 2/1 will delete all associated data.
Continue? (y/n): y
port2/1 cleared
```

Navigate to the port to verify it has been reset to factory defaults:

```
[admin@UplogixLM]# port 2/1
native
```

Use an asterisk to clear all ports on a slot. This automatically assumes there are 16 ports on the card, instead of detecting the hardware in use.

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

If you are removing an option card or virtual slot, use the **config system clear slot** command to ensure the hardware is completely cleared from the database.

```
[admin@UplogixLM]# config system clear slot 4
Slot 4 is about to be cleared.
Do you want to commit these changes? (y/n): y
```