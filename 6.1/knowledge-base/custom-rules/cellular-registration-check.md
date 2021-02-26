# Overview
This custom rule with check a cellular modem for its registration status. If the status is "Modem Registration Failed," an alarm will be generated.

# Rule

## Rules

```
rule no CellRegistrationCheck1
rule CellRegistrationCheck1
action execute -pattern "(\d,\d)" -command "AT+CGREG?" -setValue monitor CellRegistrationCheckResponse $1 -multiline
conditions
true
exit
exit

rule no CellRegistrationCheck2
rule CellRegistrationCheck2
action alarm GENERIC -a "Modem Registration Failed"
conditions
NOT compare-value monitor CellRegistrationCheckResponse = 0,1
exit
exit
```

## Scheduling

To schedule the rule, use the **config monitor** on the modem resource.

```
config monitor modem CellRegistrationCheck1 | CellRegistrationCheck2
```