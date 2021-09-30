# Overview
Local Managers can be configured to notify administrators of certain situations by email.

The system's mail system supports separate email servers for use in and out of band. IP addresses are used in place of hostnames to minimize dependence on DNS servers. SSL connections and SMTP authentication are both supported.

<div class='ucc' />Inventory > Local Manager Summary > System > Email</div>

# Configure Email Settings

Configure email settings with the interactive **config system email** command:

```
[admin@UplogixLM]# config system email
--- Existing  Values ---
In-Band SMTP Server: 127.0.0.1
In-Band from address: system@127.0.0.1
In-Band SMTP Port: 25
Use user authentication in-band: no
Prefer SSL for in-band email: no
Out-of-Band SMTP Server: 127.0.0.1
Out-of-Band from address: system@127.0.0.1
Out-of-Band SMTP Port: 25
Use user authentication out-of-band: no
Prefer SSL for out-of-band email: no
Change these? (y/n) [n]: y
--- Enter New Values ---
In-Band hostname or IP [127.0.0.1]: 10.10.10.252
In-Band from address [system@127.0.0.1]: UplogixLM@uplogix.com
In-Band SMTP Port [25]: 
Use user authentication for in-band email? (y/n) [n]: y
In-Band username: uplogixlm
In-Band password: ******
Confirm password: ******
Prefer SSL for in-band email? (y/n) [n]: y
Out-of-Band hostname or IP [127.0.0.1]: 
Out-of-Band from address [system@127.0.0.1]: 
Out-of-Band SMTP Port [25]: 
Use user authentication for out-of-band email? (y/n) [n]: 
Prefer SSL for out-of-band email? (y/n) [n]: 
Do you want to commit these changes? (y/n): y
```

The above example shows sample values.

# Testing Email Settings

You can use the **show log system** command to test your email configuration. 

```
[admin@UplogixLM]# show log system
Send log report to <support@uplogix.com>? (y/n) [y]: y
Problem sending the bug report
Underlying cause: 535 Incorrect authentication data

[admin@UplogixLM]# show log system 
Send log report to <support@uplogix.com>? (y/n) [y]: y
Problem sending the bug report
Underlying cause: Couldn't connect to host, port: 10.10.10.252; timeout 30000

[admin@UplogixLM]# show log system
Send log report to <support@uplogix.com>? (y/n) [y]: y
Bug report sent to support@uplogix.com
```

Use the **-m [email address]** argument to send a log report. If the email settings are incorrect, an error message will be displayed.

```
[admin@UplogixLM]# show log system -m djones@uplogix.com
Send log report to <djones@uplogix.com>? (y/n) [y]: 
Bug report sent to djones@uplogix.com
```