When you disconnect a device from a port, the Local Manager retains the device's configuration data. You can clear this data and return the port to its factory default configuration using the command **config system clear port** from the system resource.

```
[admin@UplogixLM]# port 1/1
AUS-CORE cisco 2610 IOS 12.2(26)
         AUS-CORE Primary Cisco Router
[admin@UplogixLM] (port1/1)]# exit
[admin@UplogixLM]# config system clear port 1/1
Clearing port1/1 will delete all associated data.
Continue? (y/n): y
port1/1 cleared
```

Navigate to the port to verify it has been reset to factory defaults:

```
[admin@UplogixLM]# port 2/1
native
```

Use an asterisk to clear all ports on a slot. This automatically assumes there are 16 ports on the card, instead of detecting the hardware in use.

```
[admin@UplogixLM]# config sys clear port 3/*
Clearing port3/* will delete all associated data.
Continue? (y/n): y
Waiting for any scheduled tasks to complete.
port3/1 cleared
Waiting for any scheduled tasks to complete.
port3/2 cleared
Waiting for any scheduled tasks to complete.
port3/3 cleared
Waiting for any scheduled tasks to complete.
port3/4 cleared
Waiting for any scheduled tasks to complete.
port3/5 cleared
Waiting for any scheduled tasks to complete.
port3/6 cleared
Waiting for any scheduled tasks to complete.
port3/7 cleared
Waiting for any scheduled tasks to complete.
port3/8 cleared
Waiting for any scheduled tasks to complete.
port3/9 cleared
Waiting for any scheduled tasks to complete.
port3/10 cleared
Waiting for any scheduled tasks to complete.
port3/11 cleared
Waiting for any scheduled tasks to complete.
port3/12 cleared
Waiting for any scheduled tasks to complete.
port3/13 cleared
Waiting for any scheduled tasks to complete.
port3/14 cleared
Waiting for any scheduled tasks to complete.
port3/15 cleared
Waiting for any scheduled tasks to complete.
port3/16 cleared
```

If you are removing an option card or virtual slot, use the **config system clear slot** command to ensure the hardware is completely cleared from the database.

```
[admin@UplogixLM]# config system clear slot 4
Slot 4 is about to be cleared.
Do you want to commit these changes? (y/n): y
```