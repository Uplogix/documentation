<!-- 5.4 -->

Returns available chassis information for a managed device.  Information returned depends on device. 

# Command availability 

CLI resource: port

Device makes: All

Uplogix Local Managers: All 

LMS offerings: All

# Syntax 

```
show chassis
```

# Usage 

```
[admin@UplogixLM (port1/1)]# show chassis
Timestamp             Current     CPU 1 Min     CPU 5 Min     Memory Total     Memory Used     Memory Free
                     CPU Util       Average       Average          (bytes)         (bytes)         (bytes)
----------------     --------     ---------     ---------     ------------     -----------     -----------
2017-06-09 10:12         0.01          0.02          0.02          7796256         2453948         5342308
2017-06-09 10:11         0.01          0.02          0.02          7796256         2453948         5342308
```

# History 

3.5 - This command was introduced.

#Related commands

- **show environment**
