# Overview
A ping monitor allows you to run the **ping** command on the managed device and apply rules to the results.

# Create a Rule (optional)

If you want to take action based on the ping results, you should create a rule. Here's an example of a rule that creates an alarm if the ping's Round Trip Time exceeds 1ms.

```
[admin@UplogixLM]# config rule pingHigh
[config rule pingHigh]# conditions
[config rule pingHigh conditions]# ping.roundTripTime max 1
[config rule pingHigh conditions]# exit
[config rule pingHigh]# action alarm GENERIC -a "Ping RTT exceeding limit"
[config rule pingHigh]# exit

[admin@UplogixLM]# show rule pingHigh
rule pingHigh
action alarm GENERIC -a "Ping RTT exceeding limit"
conditions
ping.roundTripTime max 1
exit
exit
```

# Configure the Monitor
To configure the monitor without any associated rules:

Syntax: **config monitor ping ip_address [interval]**

```
[admin@UplogixLM (port1/1)]# config monitor ping 10.10.10.1
Validate scheduled monitor(ping)?  (This will execute the job now.) (y/n): y
Job was scheduled 13: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor ping 10.10.10.1 30
```

To use the pingHigh rule with the ping monitor:

Syntax: **config monitor ping ip_address pingHigh [interval]**

```
[admin@UplogixLM (port1/1)]# config monitor ping 10.10.10.1 pingHigh
Validate scheduled monitor(ping)?  (This will execute the job now.) (y/n): y
Cancelling previous monitor for 'ping 10.10.10.1'
Job was scheduled 14: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor ping 10.10.10.1 pingHigh 30
```

> If a previous ping monitor was scheduled, it will be canceled and replaced with a new one.

If the round trip time of the ping exceeds the limit, an alarm will be generated:

```
[admin@UplogixLM (port1/1)]# show alarm
GMT       Elapsed     Device       Context     Message                  
-----     -------     --------     -------     -------------------------
18:35     0:32        AUS-CORE                  Ping RTT exceeding limit
```

## Viewing Ping Stats

```
[admin@UplogixLM (port1/1)]# show pingstats
GMT       Host           Success     Round Trip Time
-----     ----------     -------     ---------------
18:35     10.10.10.1     *           4.0 ms         
18:34     10.10.10.1     *           1.0 ms         
18:34     10.10.10.1     *           4.0 ms         
18:33     10.10.10.1     *           4.0 ms         

in the Success column, * is positive, blank is negative

```