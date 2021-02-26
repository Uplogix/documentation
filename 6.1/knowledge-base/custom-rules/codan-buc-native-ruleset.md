The following ruleset runs the VFS command on the Codan's console port and looks for a response of FAIL.  If seen, the ruleset writes FAULT to the Codan's port and sends an alert.

To schedule this ruleset to run every 30 seconds, run the command **config monitor chassis codanNative :30**.

```
config rule no codanVFS
config rule codanVFS
conditions
true
exit
action execute -command "VFS" -pattern "(FAIL)" -setValue monitor codanVFS $1 
exit

config rule no codanCheck
config rule codanCheck
conditions
compare-value monitor codanVFS = FAIL
exit
action writeStatus "FAULT"
action alarm GENERIC -a "VFS returned FAIL, faults present on Codan BUC"
exit

config ruleset no codanNative
config ruleset codanNative
rules codanVFS | codanCheck
exit
exit
```