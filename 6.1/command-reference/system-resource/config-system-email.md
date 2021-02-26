<!-- 5.4 -->

Interactive command to configure SMTP server settings for sending in-band and outband mail alerts. When alarms trigger, the Uplogix Local Manager collects them and sends them every two minutes to users who have subscribed to the alarms.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system email
```

# Usage 

For maximum fault tolerance, use separate mail servers when operating outband.

```
[admin@UplogixLM]# config system email
--- Existing  Values ---
In-Band SMTP Server: 172.16.100.1
In-Band from address: Aus01@xyzco.com
In-Band SMTP Port: 25
Use user authentication in-band: no
Prefer SSL for in-band email: no
Out-of-Band SMTP Server: 198.6.1.2
Out-of-Band from address: Aus01@xyzco.com
Out-of-Band SMTP Port: 25
Use user authentication out-of-band: no
Prefer SSL for out-of-band email: no
Change these? (y/n) [n]:

```

# In the Uplogix web interface

**Inventory > group page > System > Email** - specific to this inventory group

**Inventory > Local Manager page > System > Email** - specific to this 
system

# History 

3.4 - This command was introduced 

# Related commands 

- **show system email**
