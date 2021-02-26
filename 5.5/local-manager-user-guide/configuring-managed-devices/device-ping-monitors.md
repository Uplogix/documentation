<!-- 5.4 -->

A ping monitor allows you to run the **ping** command on the managed device and apply rules to the results.

# Create a Rule (optional)

If you want to take action based on the ping results, you should create a rule. Here's an example of a rule that creates an alarm if the ping's Round Trip Time exceeds 1ms.

```
[admin@UplogixLM]# config rule pingHigh
[config rule pingHigh]# conditions
[config rule pingHigh conditions]# ping.roundTripTime max 1
[config rule pingHigh conditions]# exit
[config rule pingHigh]# action alarm GENERIC -a "Ping RTT exceeding limit!"
[config rule pingHigh]# exit

[admin@UplogixLM]# show rule pingHigh
rule pingHigh
action alarm GENERIC -a "Ping RTT exceeding limit!"
conditions
ping.roundTripTime max 1
exit
exit
```

# Configure the Monitor

Syntax: **config monitor ping ip_address [interval]**

```
[admin@UplogixLM (port1/1)]# config monitor ping 198.51.100.1
Job was scheduled 16: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor ping 198.51.100.1 30
```

Syntax: **config monitor ping ip_address pingHigh [interval]**

```
[admin@UplogixLM (port1/1)]# config monitor ping 198.51.100.1 pingHigh
Job was scheduled 17: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor ping 198.51.100.1 pingHigh 30
```

##Viewing Ping Stats

```
[admin@UplogixLM (port1/1)]# show pingstats
UTC       Host              Success     Round Trip Time
-----     -------------     -------     ---------------
13:50     198.51.100.1      *           20.0 ms        
13:50     198.51.100.1      *           20.0 ms        
13:49     198.51.100.1      *           16.0 ms        
13:49     198.51.100.1      *           16.0 ms
```