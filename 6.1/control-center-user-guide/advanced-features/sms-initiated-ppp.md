In environments where Local Managers contact the Control Center as needed via wireless modem, contact can be initiated from the Control Center by sending an SMS message instructing a Local Manager to phone home in order to connect to the network out-of-band.

Requirements for using this capability are:

* The Local Manager uses a wireless modem (GPRS/CDMA/Iridium/Inmarsat) modem that supports SMS commands.
* The Local Manager has been configured with a phone number and SMS domain name that the Control Center can use to construct a valid SMS email address. These are locally configured with the** config answer** command.
* An SMS modem monitor with automation (i.e., a rule/ruleset) has been configured for the modem to monitor for SMS messages.  The included *smsPppOn* rule can be used in conjunction with this monitor.

To initiate contact:

1.	Select the Local Manager from the Inventory and expand the page to show the Local Manager detail.
2.	Click **Schedule Task** and from the list of tasks that may be scheduled, select **SMS Message** and click **Next**.

  ![UCC - Schedule Task - SMS](http://uplogix.com/support/docs/img/6.0/ucc-schedule-sms-task.png)
	
3.	The SMS Message - Parameters page opens. Click **Next** and the **ppp on** command is sent immediately by SMS message. It may take a few minutes before the Local Manager receives the SMS message and activates PPP to phone home.

  ![](http://uplogix.com/support/docs/img/6.0/ucc-schedule-sms-parameters.png)
 
<!-- 5.2 -->