<!-- 5.4 -->

The Control Center can be shut down or restarted from the CLI using Linux commands.

<div class='danger' />Do not remove power from the Control Center while it is running. Failure to shut down properly may result in the loss of data.</div>

Open a console or SSH session with your Control Center and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root). 

To restart the Control Center, use the **shutdown -r now** command. 

To shut down the Control Center, use the **shutdown -h** now command.

Using the **shutdown** command ensures that all services exit cleanly before the reboot / shutdown.