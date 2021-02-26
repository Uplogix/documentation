<!-- 5.4 -->

The following rules, when used in conjunction with the Local Manager's enhanced driver to manage a Riverbed device, read the status of the Riverbed and alert users to important conditions on the device.

The ruleset should be scheduled as a chassis monitor with the command **config monitor chassis RiverbedNative**.

```
config rule RiverBinfo
action execute -raw -pattern "#" -command "en\n\n"
action execute -command "show info" -pattern "Status:            (\D\D\D\D\D\D\D)" -setValue monitor ShowInfo $1 
action execute -raw -pattern "#" -command "en\n\n"
action execute -command "sh interface lan0_0 brief" -pattern "Link:               (\D\D)" -setValue monitor ShowIntLan $1 
action execute -command "sh interface inpath0_0 brief" -pattern "Up:                 (\D\D)" -setValue monitor ShowInpath $1
action execute -command "sh interface wan0_0 brief" -pattern "Link:               (\D\D)" -setValue monitor ShowIntWan $1 
action execute -raw -pattern "#" -command "term leng 0\n\n"
action execute -command "sh stat ala" -pattern "Alarm linkstate:                 (\D\D\D\D\D)" -setValue monitor LinkState $1
action execute -command "sh stat ala" -pattern "Alarm bypass:                    (\D\D\D\D\D)" -setValue monitor ByPassState $1
conditions
console.dsr equals True
exit
exit

config rule RiverBinfo1
action alarm -a "service Degraded"
action writeStatus "Service Degraded"
action clearValue monitor ShowInfo
conditions
compare-value monitor ShowInfo = Degrade
exit
exit

config rule RiverBinfo2
action alarm -a "service Critical"
action writeStatus "Service Critical"
action clearValue monitor ShowInfo
conditions
compare-value monitor ShowInfo = Critica
exit
exit

config rule RiverBinfo3
action writeStatus "Service Healthy"
action clearValue monitor ShowInfo
conditions
compare-value monitor ShowInfo = Healthy   
exit
exit

config rule RiverBinpath1
action alarm -a "inpath down"
action clearValue monitor ShowInpath
conditions
compare-value monitor ShowInpath = no
exit
exit

config rule RiverBintLan1
action alarm -a "Lan0_0 link down"
action clearValue monitor ShowIntLan
conditions
compare-value monitor ShowIntLan = no
exit
exit

config rule RiverBintWan1
action alarm -a "Wan0_0 link down"
action clearValue monitor ShowIntWan
conditions
compare-value monitor ShowIntWan = no
exit
exit

config rule RiverBLinkS1
action alarm -a "Link State ERROR"
action clearValue monitor LinkState
conditions
compare-value monitor LinkState = ERROR
exit
exit

config rule RiverByPass1
action alarm -a "Bypass State ERROR"
action clearValue monitor ByPassState
conditions
compare-value monitor ByPassState = ERROR
exit
exit

config ruleset RiverbedNative
description null
rules
RiverBinfo | RiverBinfo1 | RiverBinfo2 | RiverBinfo3 | RiverBintLan1 | RiverBinpath1 | RiverBintWan1 | RiverBLinkS1 | RiverByPass1
exit
exit
```