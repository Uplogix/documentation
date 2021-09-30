<!-- 5.4 -->

Sends the Uplogix Local Manager's internal processing log. Useful mostly to the Uplogix support team, it requires the system's email settings to be set up (configured with **config system email**). It is encrypted and cannot be displayed to the screen. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

#Syntax 

```
show log system [-m <"emailaddress">] [-n <#>] [-s <"subject">]
```

**-m <"emailaddress">** - Email the report to the address given.
**-n <#>** - Specify the number of logs to include. Default is 20.
**-s <"subject">** - Specify the subject line of the email.

# Usage
```
[admin@UplogixLM]# show log system
Send log report to <support@uplogix.com>? (y/n) [y]: y
Bug report sent to support@uplogix.com
```

```
[admin@UplogixLM]# show log system -m admin@uplogix.com
Send log report to <admin@uplogix.com>? (y/n) [y]: y
Bug report sent to admin@uplogix.com
```
# History 

3.4 - This command was introduced to replace the show log Local Manager command.

# Related commands 
--
