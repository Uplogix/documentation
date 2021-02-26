<!-- 5.4 -->

Display pass-through, SSH port forwardding, and terminal shadow settings for the current resource.

# Command availability 

CLI resource: port, modem, powercontrol

Device makes: All

Modem: All

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show protocols <forward | pass-through | shadow>
```

# Usage 
```
[admin@UplogixLM (port1/1)]# show protocols pass-through
SSH pass-through port: 2001
```
```
[admin@UplogixLM (port1/1)]# show protocols shadow
Enable: false
Using system management IP: 198.51.238.102
Port: 0
```
```
[admin@uplogixLM (port1/1)]# show protocols forward
forward management 80 http

```

# Related commands 

**config protocols shadow**
**config protocols pass-through**
**config protocols forward**