<!-- 5.4 -->

Displays collected data from SLV tests. 

A valid SLV license must be applied to access this command. Licenses are managed on the Uplogix Control Center. 

# Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: Advanced

# Syntax 

```
show slv stats <testName> [-n <#>] [-v] [-x]
```

**-n <count>** - Maximum number of records
**-v **- Verbose display
**-x** - Execute now - runs SLV test without scheduling it and displays the results in verbose format.

# Usage 

By default, this command returns the 20 most recent entries. To view more, or less, use the -n parameter and include a number to display.

```
[admin@UplogixLM]# show slv stats Server
UTC       Test       Connect     Message
-----     ------     -------     -------
12:53     Server     12                 
12:48     Server     14                 
12:43     Server     11                 
12:38     Server     11                 
12:33     Server     12                 
12:28     Server     13                 
12:23     Server     11           
```

```
[admin@UplogixLM]# show slv stats NextHopRouter -x
UTC       Test           Connect     Message
-----     ----------     -------     -------
18:51     NextHopRou     1                  
```

# In the Uplogix web interface

**Inventory > Local Manager page > SLV Stats** - specific to this system

#History 
2.5 - This command was introduced.
2.6 - Execute Now (-x) featured added.

# Related commands 

- **config slv http**
- **config slv ipt**
- **config slv tcp**
- **show slv test**
