#Description

This alarm typically indicates that the LM is having trouble logging into a managed device. 


#Steps to Resolve

The steps to clear the alarm involve determining why the Local Manager can't successfully log in into the managed device.

## Are the login credentials correct?

The most common reason for this alarm is having the wrong username/password configured when first <a href="http://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/initializing-ports">initializing the port</a>.

To confirm that the Local Manager can't log into your managed device, open up 2 SSH sessions to the LM. In the first session, navigate to the port that's getting the alarm and run the **terminal shadow** command. This will show you the raw console communication between the LM and the devices. In the other window navigate to the same port and run **terminal**. Then, watch the first window. If you see "invalid password" or "access denied" or the like, then the authentication settings will need to be updated on the LM.

Here are example results from a terminal shadow session returning an incorrect password:


<pre>
<code>
MANAGED-DEVICE>show privilege 
Current privilege level is 1 
MANAGED-DEVICE> 
MANAGED-DEVICE> 
MANAGED-DEVICE>show privilege 
Current privilege level is 1 
MANAGED-DEVICE> 
MANAGED-DEVICE> 
MANAGED-DEVICE>terminal length 0 
MANAGED-DEVICE> 
MANAGED-DEVICE> 
MANAGED-DEVICE>show privilege 
Current privilege level is 1 
MANAGED-DEVICE>enable 
Password: 
% Access denied
</code>
</pre>

Use ~[ENTER] to get out of terminal shadow, and then use the **config authentication** command to configure Console and Enable user names and passwords.





