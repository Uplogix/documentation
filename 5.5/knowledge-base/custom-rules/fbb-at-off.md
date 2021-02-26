The following rules are designed to comunicate with a FBB unit over an Uplogix virtual serial port.  They query the state of the FBB unit for active data sessions, and if they see one for 60 minutes they send a command to shut the data session off.

```
config rule no fbbCheck
config rule fbbCheck
description this rule sends "at+cgact=?" to the FBB at interface and collects the response
conditions
true
exit
action execute -command "at+cgact=?" -pattern "(\D\D\D\D\D\D\D\D\D\D\D\D\D)" -setValue system fbbStatus $1
exit

config rule no fbbOff
config rule fbbOff
description this rule looks for "+CGACT: (0,1)" in the response and turns off FBB after seeing it for an hour
conditions
compare-value system fbbStatus = +CGACT: (0,1) :60i
exit
action execute -command "at+cgact=0,1" -pattern "#"
action event GENERIC -a "FBB shut off"
action clearValue system fbbStatus
exit
```

To schedule this ruleset, run the following command on the FBB's AT port: **config monitor chassis fbbCheck | fbbOff :60**