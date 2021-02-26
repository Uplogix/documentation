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
Timestamp      Current     CPU 1 Min     CPU 5 Min     Memory Total     Memory Used     Memory Free
              CPU Util       Average       Average          (bytes)         (bytes)         (bytes)
---------     --------     ---------     ---------     ------------     -----------     -----------
15:30:44           0.0           0.0           0.0         46570436         2397692        44172744
15:30:14           0.0           0.0           0.0         46570436         2397648        44172788
15:29:44           0.0           0.0           0.0         46570436         2397592        44172844
15:29:14           0.0          0.01           0.0         46570436         2397588        44172848
15:28:44          0.03          0.01          0.01         46570436         2397608        44172828
15:28:14           0.0          0.01           0.0         46570436         2397732        44172704
15:27:44           0.0           0.0           0.0         46570436         2397880        44172556
```

# History 

3.5 - This command was introduced.

#Related commands

- **show environment**
