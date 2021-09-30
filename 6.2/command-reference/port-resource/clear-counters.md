<!-- 5.4 -->

Counters on a device usually increase over time and can mask potential problems if left to accumulate. The **clear counters** command clears all interface counters on the device. Rules can be defined to automate this operation using the *clearCounters* action.

# Command availability 
CLI resource: port

Device makes: Alcatel, Cisco, Juniper, Netscreen, TippingPoint

Uplogix Local Managers: All

LMS offerings: All

# Syntax 
```
clear counters
```
# Usage 

~~~
[admin@UplogixLM (port1/1)]# clear counters
Interface counters successfully cleared
~~~

# In the Uplogix web interface

**Schedule > Scheduled Tasks** - all devices that match the selected filter

**Inventory > Local Manager page > port detail > schedule button** - specific to this device

# History 

--

# Related commands 

- **clear log**
