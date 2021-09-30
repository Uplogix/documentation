<!-- 5.4 -->

Opens an editor to create a Service Level Verification (SLV) HTTP test that can be scheduled using a monitor. 

A valid SLV license must be applied to access this command. Licenses are managed on the Uplogix Control Center. 

# Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: Advanced

# Syntax 

```
config slv http [no] <"testname">

```

# Usage 

```
[admin@UplogixLM]# config slv http xyzcoWebServer
[config slv http xyzcoWebServer]# 
[config slv http xyzcoWebServer]# url http://www.xyzco.us.com
```

# In the Uplogix web interface

**Inventory > Local Manager page > Automation > SLV Tests** - specific to this system

# History 

2.5 - This command was introduced.

# Related commands 

- **show slv http**
- **show slv test**
- **show slv stats**
