<!-- 5.4 -->

Displays configured SLV tests. To view test results, use the show slv stats command.

A valid SLV license must be applied to access this command. Licenses are managed 
on the Uplogix Control Center. 

#Command availability 

CLI resource: system

Uplogix Local Managers: All

LMS offerings: Advanced

# Syntax 

```
show slv test <â€œtestNameâ€ | *>
```

# Usage 

Specify the name of the test, or use * to display all tests.
```
[admin@UplogixLM]# show slv test *
TCP tests:
slv tcp NextHopRouter
host 198.51.235.94
tcpPort 22
exit

HTTP tests:
No SLV HTTP tests were found for '*'.

IPT tests:
slv ipt xyzcoVoip
call type sip
codec g711u
destination ip 192.168.1.104
duration 20
payload harvardmale
exit
```

In the Uplogix web interface

**Inventory > Local Manager page > SLV Stats** - specific to this system

# History 
2.5 - This command was introduced.

# Related commands 

- **config slv http**
- **config slv ipt**
- **config slv tcp**
- **show slv stats**
