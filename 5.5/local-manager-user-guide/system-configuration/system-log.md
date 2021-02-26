<!-- 5.4 -->

The Local Manager's system log contains useful information for troubleshooting. When you contact Uplogix Support about an issue, they may ask for the system log. This page describes the various ways to view, access, and offload that information.

# Send Logs to Uplogix Support

You can use the **show log system** command to email the system log to Uplogix Support (support@uplogix.com). The Local Manager has to be able to send email for this feature to work (configured with **config system email**).

```
[admin@UplogixLM]# show log system
Send log report to <support@uplogix.com>? (y/n) [y]: y
Bug report sent to support@uplogix.com
```

To view the contents of the email, or to send the system log to a different email address, use the **- m [email address]** argument.

```
[admin@UplogixLM]# show log system -m admin@uplogix.com
Send log report to <admin@uplogix.com>? (y/n) [y]: y
Bug report sent to admin@uplogix.com
```

If the Local Manager is not configured to send email, you will see the following message:

```
[admin@UplogixLM]# show log system
Send log report to <support@uplogix.com>? (y/n) [y]: y
Problem sending the bug report
Underlying cause: Could not connect to SMTP host: 127.0.0.1, port: 25
```

# Send Log to SCP / FTP server

The hidden **show_envoy_log** command displays the contents of the system log to the screen. Using the pipe (**|**) argument, you can redirect the output to a file and transfer that file to an SCP or FTP server.

```
[admin@UplogixLM]# show_envoy_log | scp emsadmin@172.30.105.8:UplogixLM.log
emsadmin@172.30.105.8's password: ********
Copy succeeded.
```

Only a few pages of the log are sent by default. To send more, specify a number of lines by including an integer after **show_envoy_log**.

```
[admin@UplogixLM]# show_envoy_log 10000 | scp emsadmin@172.30.105.8:UplogixLM.log
emsadmin@172.30.105.8's password: ********
Copy succeeded.
```

# Save Session Log to Desktop

These instructions are written for PuTTY, but they can be applied to any SSH client that can produce a session log. 

1. Open PuTTY
2. Under *Session*, *Logging*, change Session Logging to *All session output*
3. Connect to the Local Manager and log in
4. Run **config system page-length** and change the page-length setting to 100000
5. Run **show_envoy_log** or **show_envoy_log 10000**
6. Exit PuTTY
7. Send the log file to Uplogix Support (support@uplogix.com)