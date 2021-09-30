<!-- 5.4 -->

Displays the Uplogix Local Manager's current email notification and server settings. These are used to send alert messages to subscribed users.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

#Syntax 

```
show system email
```

# Usage 

```
[admin@UplogixLM]# show system email
In band SMTP Server IP Address: 10.100.2.178
In band FROM address: xyzcoaus01@xyzco.us.com
In band SMTP Port: 25
Use user authentication in band: yes
Username: xyzcoAus01
Password: ********
Use SSL encryption: yes
Out of band SMTP Server IP Address: 4.183.2.201
Out of band FROM address: xyzcoaus01@xyzco.us.com
Out of band SMTP Port: 25
Use user authentication out of band: yes
Username: xyzcoAus01
Password: ********
Use SSL encryption: yes
```

# In the Uplogix web interface

**Inventory > group page > System > Email** - specific to this inventory group

**Inventory > Local Manager page > System > Email** - specific to this system

# History 
3.4 - This command was introduced to replace show Local Manager email.

# Related commands 

- **config system email**
