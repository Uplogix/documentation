<!-- 5.4 -->

This rule is designed to run on a unix / linux server that is printing log messages to the console. The rule watches what comes across the console from the server using the "terminal.line" condition, and if it sees the message "Kernel panic" it sends an alarm to notify you of the condition.

```
config rule kernelPanic 
description kernel panic message seen on the console 
action alarm GENERIC -a "Kernel panic" 
conditions 
terminal.line matches "Kernel panic" 
exit 
exit
```

To schedule this rule, go to the port on your Local Manager with a \*nix server, and run the command **config monitor terminal kernelPanic**.