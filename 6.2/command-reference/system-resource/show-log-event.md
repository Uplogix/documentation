<!-- 5.4 -->

Displays the Uplogix Local Manager's log of automated events, user actions, and other threshold issues.

# Command availability 

CLI resource: system, port, modem

Device makes: All

Modem: All

Uplogix system : All

LMS offerings: All

# Syntax 

```
show log event [-l <level>] [-m <"email">] [-n <#>]
```
**-l <level>** - Syslog level
**-m <"email">** - Email address to send report
**-n <#>** - Max number of messages

# Usage 

```
[admin@UplogixLM]# show log event
GMT      L Context            Message
-------- - ------------------ -------------------------------------------------------------------
10/01 14 5 admin@172.30.5.164 User logged into Envoy.
10/01 14 5 admin@172.30.5.164 User logged out of Envoy. (Envoy detected user session closed.)
10/01 15 5 admin@172.30.5.164 User logged into Envoy.
10/01 15 5 admin@172.30.5.164 User logged out of Envoy. (Envoy detected user session closed.)
10/01 16 5 admin@172.30.5.164 User logged into Envoy.
10/01 16 5 admin@172.30.5.164 User started a terminal session.
10/01 16 5 admin@172.30.5.164 User logged out of Envoy. (Envoy detected user session closed.)

```

# History 

2.0 - This command was introduced.

# Related commands 

- **show events**

