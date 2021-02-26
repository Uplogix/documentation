<!-- 5.4 -->

Used to pull ad-hoc files from managed device. The files are compared to the versions previously stored. If the content is different, the version stored as current is moved to previous, overwriting the existing previous version, and the new file is stored as current. 

The command line defined as the [remoteCmd] will be issued to the device and the tftp/sftp server will be started on the management IP address of the Local Manager 

Rules can be defined to automate this operation using the pull action.

# Command availability

CLI resource: port, powercontrol

Device makes: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
Pull <tftp | sftp> [dedicated] "<remoteCmd>" <xferFileName> <type> [version]
```

Add **dedicated** to use dedicated ethernet

**remoteCmd** is executed on the device

**xferFileName** of incoming file

**type** = &lt;os | running-config | startup-config | show-tech | post | scratch&gt;

**version** = &lt;candidate | current | previous | <customVersion> &gt;

# Usage 

The command used to tftp the file FROM the managed device is sent inside the quotes. If no version is specified it will be stored in â€œCurrentâ€.


```
[admin@UplogixLM (port1/1)]# pull tftp "tftp 2.3.4.5 -c put /tmp/t.txt" t.txt running-config.
```

# History 

4.4 - This command was introduced

# Related commands 

- **push**