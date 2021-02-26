# Overview
Uplogix recommends the use of service or functional accounts when managed devices. This allows the Local Manager to run commands in privileged mode without affecting the privileges or auditing of other users. Most customers create a functional account with full Level 15 privileges. However, if your security policy requires that each IOS command be explicitely granted, this list contains all of the commands that the Uplogix Cisco IOS Advanced Driver users to monitor and manage Cisco devices.

# exec commands
* show privilege
* terminal length
* show interface
* show processes cpu
* show processes memory
* show version
* reload
* show startup-config
* show running-config
* copy
* show tech-support
* dir
* delete
* ?
* verify
* exit
* show file systems
* more
* show bootvar
* config terminal
* write memory
* show ip interface
* request platform software package clean *
* request platform software package expand *
* show switch *
* show logging +
* terminal pager +
* show cpu usage +
* show curpriv +

\*: IOS-XE Version 16+ ONLY

+: ASA environment


# config commands
* no logging monitor
* no logging buffered
* line con 0
* logging synchronous
* exit
