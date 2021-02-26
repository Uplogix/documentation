<!-- 5.5.4 -->
<!-- Custom rules that examine SLV http tests and alert if necessary. -->

These rules examine the results from an SLV (service level verification) test run by an Uplogix local manager for results that indicates that the test failed, and send email alerts to notify users subscribed to alerts on the Uplogix local manager in question.

To load them onto your Uplogix Local Manager, simply copy and paste the below rules into the CLI.

```
config rule httpResponseZeroes
description this rule sends an alarm if the http slv test receives 0 for all round trip metrics
action alarm GENERIC -a "http test returned 0 on all metrics"
conditions
slv.timeToConnect equals 0 AND
slv.timeToFirstByte equals 0 AND
slv.timeToLastByte equals 0
exit
exit
 

config rule httpResponseConnectionRefused
description this rule sends an alarm if the http slv test receives a 'connectionrefused' response
action alarm GENERIC -a "http test returned 'Connection refused'"
conditions
slv.message equals "Connection refused"
exit
exit

config ruleset httpSLVErrors
description null
rules
httpResponseConnectionRefused | httpResponseZeroes
exit
exit
```

To apply the rules, attach them to a SLV test on the Uplogix local manager with the **config monitor** command (for example: **config monitor slv webtestexample httpSLVErrors :500**).

## Demo

Create an SLV http test following the instructions in [Service Level Verification](https://uplogix.com/docs/local-manager-user-guide/advanced-features/service-level-verification).

```
[admin@UplogixLM]# config slv http uplogixedu
[config slv http uplogixedu]# url uplogix.edu
[config slv http uplogixedu]# exit
```

Configure a monitor using the created SLV http test and the new httpSLVErrors ruleset.

```
[admin@UplogixLM]# config monitor slv uplogixedu httpSLVErrors
Validate scheduled monitor(slv)?  (This will execute the job now.) (y/n): y
Job was scheduled 2: [Interval: 00:00:30 Mask: * * * * *] rulesMonitor slv uplogixedu httpSLVErrors 30
```

View the alarms with the **show alarm** command.

```
[admin@UplogixLM]# show alarm
GMT       Elapsed     Device     Context        Message                             
-----     -------     ------     ----------     ------------------------------------
18:22     0:22                   uplogixedu      http test returned 0 on all metrics
```
