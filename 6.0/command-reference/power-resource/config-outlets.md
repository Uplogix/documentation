<!-- 5.4 -->

Interactive command to associate power outlets with the ports that they power.

# Command availability 

CLI resource: powercontrol

Power controllers: All

Uplogix Local Managers: All

LMS offerings: All

#Syntax 

```
config outlets
```

# Usage 

```
[admin@UplogixLM (powercontrol)]# config outlets
--- Existing  Values ---
Change these? (y/n) [n]: y
--- Enter New Values ---
Would you like to add a new mapping? (y/n) [n]: y
Outlet:1
Interface:port1/1
Would you like to add a new mapping? (y/n) [n]: y
Outlet:4
Interface:port1/2
Would you like to add a new mapping? (y/n) [n]: n
Do you want to commit these changes? (y/n): y
[admin@UplogixLM (powercontrol)]# show outlets
Outlet 1 goes to interface port1/1
Outlet 4 goes to interface port1/2
```

# History 

--

# Related commands 

- **on**
- **off**
- **power**
- **show outlets**
