<!-- 5.4 -->

When licensed for each Local Manager, the Service Level Verification (SLV) module ensures consistent, high levels of IT service by synthetically measuring the performance of critical network services and applications from the end-userâ€™s perspective and comparing the results to drive automation decisions.

You can use SLV to execute Voice over IP (VoIP) calls, web transactions, and TCP SYN/ACK handshakes to verify end-to-end network functionality.

This topic focuses on the activation, configuration, and usage of SLV in a Local Manager CLI environment. 

# Service Level Verification Tests

There are three types of SLV tests available:

## Web-based Transactions

This test performs an HTTP request from the Local Manager to a remote destination. DNS lookup, connection setup time, time to first byte, and time to last byte are measured. Also collected are the HTTP result code and the first 1,024 bytes of HTML for further validation testing.

## TCP/IP SYN/ACK

Often called a TCP handshake, the round-trip connection establishment process more accurately measures the network portion of communication by isolating much of the delay associated with the network itself, leaving out the overhead of the application layer. This test has the smallest network impact.

## VoIP / IP Telephony (IPT)

For IPT environments, the Local Manager captures 47 specific RTP Control Protocol (TRCP) metrics that characterize the network's ability to transport VoIP traffic. Pre-encoded voice calls with phonetically balanced Harvard sentences are used to gauge VoIP performance. Metrics such as jitter, latency, packet loss, MOS scores, and R values can be evaluated by the Local Manager's rules engine.

# Installing an SLV License

Service Level Verification is an optional, add-on feature available for purchase from Uplogix. Contact your account executive or [support@uplogix.com](mailto:support@uplogix.com) for more information.

Once you have purchased a license, you will need to [install it on the Control Center](/docs/control-center-user-guide/managing-the-control-center/licenses). 

# Creating SLV Tests

<div class='ucc' />Inventory > Local Manager Summary > Automation > SLV Tests</div>

Use the **config slv** command with either **http**, **tcp**, or **ipt** as a secondary argument to create SLV tests. Use the **?** subcommand to view available editor options.

Syntax:

```
config slv <type> <testname>
```

> SLV test names can only contain alphanumeric characters.

## HTTP

Use the **config slv http {testname}** command to create an HTTP test.

```
[super@UplogixVLM]# config slv http uplogixtest
[config slv http uplogixtest]# ?
SLV HTTP config options are:
url url
show
exit
```

Use the **url** subcommand to specify a target. Both IP addresses and hostnames can be used. However, hostnames require [configuration of DNS](http://uplogix.com/docs/local-manager-user-guide/system-configuration/ip-addressing).

```
[config slv http uplogixtest]# url uplogix.com
[config slv http uplogixtest]# exit
```

You can view your test with the **show slv** command.

```
[super@UplogixVLM]# show slv http uplogixtest
slv http uplogix.com
url http://uplogix.com
exit
```

## TCP

Use the **config slv tcp testname** command to create a TCP test.

```
[super@UplogixVLM]# config slv tcp supportssh     
[config slv tcp supportssh]# ?
SLV TCP config options are:
host <host>
tcpPort <tcpPort>
show
exit

[config slv tcp supportssh]# host 172.30.4.227  
[config slv tcp supportssh]# tcpPort 22
[config slv tcp supportssh]# exit
```

## IPT

Use the **config slv ipt testname** command to create an IPT test.

```
[super@UplogixVLM]# config slv ipt voiptest
[config slv ipt voiptest]# ?
SLV IPT config options are:
call type < sip >
codec < g711u | g711a | g728 | g729a | g729e >
destination ip <destination ip>
duration <1-600>
payload < harvardfemale | harvardmale | dtmf1 | dtmf2 | dtmf3 | dtmf4 | dtmf5 | dtmf6 | dtmf7 | dtmf8 |
 dtmf9 | 1khz | 2khz | 3khz >
show
exit

[config slv ipt voiptest]# call type sip
[config slv ipt voiptest]# codec g711a
[config slv ipt voiptest]# destination ip 172.30.152.116
[config slv ipt voiptest]# duration 15
[config slv ipt voiptest]# payload harvardfemale
[config slv ipt voiptest]# exit
```

A separate Local Manager can be used as an IPT endpoint. To configure it, see [IPT Listener](#ipt-listener).

# Scheduling SLV Tests

SLV tests are run by the SLV monitor, which is similar to other monitors such as modem, gps, and chassis. SLV monitors take two arguments:

* SLV test - required, specifies which SLV test to run
* Rule(s) or Ruleset(s) - optional, take action based on SLV test results

Use the **config monitor slv** command to schedule a monitor.

Here is the syntax:

```
[super@UplogixVLM]# config monitor slv
usage: monitors <slv {testName} | system> {ruleList} {:[delay seconds]}

ruleList - rule names separated by comma or bar
delay seconds - time between executions
ex. config monitors slv httpTest rule1, rule2 | rule3 :30
```

For example:

```
[super@UplogixVLM]# config monitor slv uplogixtest
Validate scheduled monitor(slv)?  (This will execute the job now.) (y/n): y
Job was scheduled 1: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor slv uplogixtest 30
```

The above example schedules the uplogixtest (HTTP test) we created earlier. The **config monitor slv** command does not need to be told what type of SLV test you are using.

# Viewing SLV Test Results

<div class='ucc' />Inventory > Local Manager Summary > SLV Stats</div>

Use the **show slv stats** command to view collected stats on SLV tests.

Here is the syntax:

```
[super@UplogixVLM]# show slv stats
usage: stats <testName> [options]

--- options ---

  -n <count>  Maximum number of events
  -v          Verbose display
  -x          Execute now
```

To view the stats of the HTTP uplogixtest test we scheduled earlier, run **show slv stats uplogixtest**.

```
[super@UplogixVLM]# show slv stats uplogixtest
CDT    Test        IP Address   Connect  1st Byte  Last Byte  # Bytes  HTTP Response  Message
-----  ----------  -----------  -------  --------  ---------  -------  -------------  -------
09:22  uplogixtes  45.56.74.20  7        388       470        300691   200 OK                
09:21  uplogixtes  45.56.74.20  8        348       415        300686   200 OK                
09:21  uplogixtes  45.56.74.20  8        363       428        300681   200 OK                
09:20  uplogixtes  45.56.74.20  8        453       3679       300706   200 OK                
09:20  uplogixtes  45.56.74.20  12       463       3804       300691   200 OK                
09:19  uplogixtes  45.56.74.20  15       422       515        300706   200 OK
```

# Adding Rule(s) and Ruleset(s)

<div class='ucc' />Inventory > Inventory Group > Automation > Rules</div>
<div class='ucc' />Inventory > Local Manager Summary > Automation > Rules</div>

To take action based on the results of SLV tests, we'll need to create some rules that look at the collected data.

In this example, we will create a rule that triggers on a maximum time to connect. If the time to connect exceeds the threshold, we'll create an alarm.

```
[super@UplogixVLM]# config rule uplogixslow
[config rule uplogixslow]# conditions   
[config rule uplogixslow conditions]# slv.timeToConnect max 7       
[config rule uplogixslow conditions]# exit
[config rule uplogixslow]# action alarm -a "Uplogix website is slow"
[config rule uplogixslow]# exit
```

> **TIP:** If you are unsure which actions and variables are available for rules, consider using the Control Center's Rules pages, as they list all of the options in convenient drop-down menus.

To apply the rule to a new or existing SLV monitor, use the **config slv monitor** command.

```
[super@UplogixVLM]# config monitor slv uplogixtest uplogixslow
Validate scheduled monitor(slv)?  (This will execute the job now.) (y/n): y
Cancelling previous monitor for 'slv uplogixtest'
Job was scheduled 2: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor slv uplogixtest uplogixslow 30
```

You can see if the rule's condition was met by running **show alarms**.

```
[super@UplogixVLM]# show alarms
CDT       Elapsed     Device     Context         Message                 
-----     -------     ------     -----------     ------------------------
09:34     0:28                   uplogixtest      Uplogix website is slow
```

# IPT Listener

If there are no IPT endpoints in your network, you can still use the IPT tests by turning on the IPT Listener feature on your Local Manager.

Use the **config system ipt** command to enable the listener.

```
[super@UplogixVLM]# config system ipt
[config system ipt]# ?
Allowable arguments are:
show
[no] subinterface
duration
endpoints
[no] listen
payload
[no] allow
[no] deny
or 'exit' to quit config mode

[config system ipt]# listen <-- REQUIRED to enable listener
[config system ipt]# payload harvardmale
[config system ipt]# allow all
[config system ipt]# duration 15
[config system ipt]# exit
```
