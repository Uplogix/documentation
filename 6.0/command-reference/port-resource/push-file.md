<!-- 5.4 -->

Used to push ad-hoc files to the managed device from the Local Manager. 

The command line defined as the [remoteCmd] will be issued to the device and the tftp/sftp server will be started on the management IP address of the Local Manager 

Rules can be defined to automate this operation using the push action.

# Command availability

CLI resource: port, powercontrol

Device makes: All

Uplogix Local Managers: All

LMS offerings: All

# Syntax

```
Push <tftp | sftp> [dedicated] "<remoteCmd>" <xferFileName> <type> [version]
```   

Add **dedicated** to use dedicated ethernet

**remoteCmd** is executed on the device

**xferFileName** of outgoing file

**type** = <os | running-config | startup-config | show-tech | post | scratch>

**version** = <candidate | current | previous | <customVersion> >

# Usage 

The command used to tftp the file FROM the managed device is sent inside the quotes. If no version is specified it will be stored in â€œCurrentâ€.


```
[admin@UplogixLM (port1/1)]# push tftp "tftp 2.3.4.5 -c get p1os.bin" p1os.bin os upgrade45
```

# History 

4.5 - This command was introduced

# Related commands 

**pull**