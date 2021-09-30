<!-- 5.5.4 -->

<div class='ucc' />Inventory > Local Manager Summary > System > Email</div>
 
Local Managers can be configured to notify administrators of certain situations by email.

The system's mail system supports separate email servers for use in and out of band. IP addresses are used in place of hostnames to minimize dependence on DNS servers. SSL connections and SMTP authentication are both supported.

Configure email settings with the interactive **config system email** command:

```
[admin@UplogixLM]# config system email
--- Existing Values ---
>> output removed <<
--- Enter New Values ---
In band IP [127.0.0.1]: 192.168.1.245
In band from address [system@127.0.0.1]: UplogixLM@uplogix.com
In band SMTP Port [25]: 
Use user authentication for in band email? (y/n) [n]: y 
In band username: UplogixLM
In band password: *******
Confirm password: *******
Prefer SSL for in band email? (y/n) [n]: n
Out of band IP [127.0.0.1]: 
Out of band from address [system@127.0.0.1]: 
Out of band SMTP Port [25]: 
Use user authentication for out of band email? (y/n) [n]: 
Prefer SSL for out of band email? (y/n) [n]: 
Do you want to commit these changes? (y/n): y
```

The above example shows sample values.

You can use the **show log system** command to test your email configuration. Use the **-m [email address]** argument to send a log report. If the email settings are incorrect, an error message will be displayed.

```
[admin@UplogixLM]# show log system -m support@uplogix.com
Send log report to <support@uplogix.com>? (y/n) [y]: y
Problem sending the bug report
Underlying cause: 535 Incorrect authentication data

[admin@UplogixLM]# show log system -m support@uplogix.com
Send log report to <support@uplogix.com>? (y/n) [y]: y
Bug report sent to support@uplogix.com
```