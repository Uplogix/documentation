<!-- 5.4 -->

Shows ping results from the current port. 

# Command availability 

CLI resource: port

Device makes: Cisco, iDirect, Foundry, Juniper

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
show pingstats [-all | -n <#>]
```

**-all **â€“ All ping results
**-n <#>** - Maximum number of ping results

# Usage 
In the Success column, * represents a positive result; blank is negative

```
[admin@UplogixLM (port1/1)]# show pingstats
UTC       Host              Success     Round Trip Time
-----     -------------     -------     ---------------
13:50     198.51.100.1      *           20.0 ms        
13:50     198.51.100.1      *           20.0 ms        
13:49     198.51.100.1      *           16.0 ms        
13:49     198.51.100.1      *           16.0 ms    
```

# History 
--

# Related commands 

- **show interface**
