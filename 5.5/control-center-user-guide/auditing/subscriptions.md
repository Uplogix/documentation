<!-- 5.4 -->

# Overview

To provide subscribed information, alerts and reports, the Control Center must be configured to send email. For more information, see [Mail Settings](https://uplogix.com/docs/control-center-user-guide/managing-the-control-center/mail-settings "Mail Settings").

To receive alerts from Local Managers and reports from the Control Center, the user account must be:

- configured with an email address where alerts from the Local Managers and reports from the Control Center can be received
- subscribed to the desired alerts and reports

To audit other accounts, the account must be:

- configured with an email address where alerts and reports are received from the Control Center
- configured to audit at least one other account
- subscribed to the appropriate session report (hourly, daily, weekly, or monthly) for the account to be audited

These can be configured on the Create/Edit User or Create/Edit Group pages. Click the right arrows   to expand the collapsed sections of these pages.

# Configuring an Account to Receive Email

<div class='ucc' />Administration > Users > Username > Edit User</div>

For an account to receive alerts (from Local Managers) or reports (from the Control Center) by email, at least one email address where the user can receive alerts and reports (including user audits) must be entered.

Edit a user account and click *Add* under *Email Addresses*.

![Uplogix Control Center - Add Email](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-add-email.png)

The in-band and out-of-band settings only apply to information that Local Managers email to you. By default, the address entered is used in both situations.

Select *Terse* to limit the message to a subject line only. Use the Terse setting for email directed to a pager or cell phone. Click *Add Email* when all the email information has been entered and then *Save* on the edit user details screen.

> To remove an email address, use the *Remove* button rather than manually clearing the address field.

# Configuring the account to audit others and to be audited

To receive some reports, a user account must be set up to audit other accounts. Learn more about it under Auditing > [Users](http://uplogix.com/docs/control-center-user-guide/auditing/users)

# Subscribing to alerts

<div class='ucc' />Administration > Users > Username > Edit</div>

Individual user accounts may subscribe to alerts.

Subscribe the account to alerts on the desired resources.

- Subscription resources are individual ports, modem, powercontrol, system, or all.
- Sub-resources are interface, chassis, or all.
 
![Uplogix Control Center - Alert Subscriptions](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-alert-subscriptions.png)

Click *Save* at the top or bottom of the page when finished setting up the account information.

# Alert Options

<div class='ucc' />Administration > Users > User ID > Alert Subscriptions > Alert Options</div>

By default, alerts are emailed to subscribed users every two minutes while they are active.

Limit the number of alerts that a user receives with the Alert Options settings on the Alert Subscriptions page.
 
![Uplogix Control Center - Alert Options](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-alert-options.png)
â€ƒ
*Alert Options* specify the times, days, and frequency when alerts may be emailed to this user. The limit options are as follows. Leave the wildcard * character in the fields you do not wish to restrict.

|Option	|Description|
|:--|:--|
|Days of the week	|Limit the receipt of alerts to certain days of the week. Specify the range of days numerically with 1 representing Monday.<br><br>For example, if the user should only receive alerts from Friday through Monday, enter 5-1.|
|Months of the year	|Limit the receipt of alerts to certain months. Specify the beginning and ending month by number.<br><br>For example, if the user should only receive alerts from September through May, enter 9-6.|
|Days of the month	|Limit the receipt of alerts to certain days of the month. Specify which days by number.<br><br>For example, if the user is on call only from the 16th to the end of the month, enter 16-31.|
|Hours	|Hours are specified in UTC time.<br><br>Limit the receipt of alerts to a specific time of day. Specify start and end time.<br><br>For example, if the user is in the US central time zone (UTC -6:00) and  needs to receive alerts generated between 5 p.m. and midnight, convert these times to UTC (00:00 to 06:00) and enter the hours as 23-6.|
|Minutes	|Limit the receipt of alerts to a specific part of each hour. Specify the start and end minutes.<br><br>For example, if the user should only receive alerts during the first 15 minutes of every hour, enter 00-15.|
|Frequency	|Set how often the Control Center sends alerts. Alerts can be sent as seldom as every 120 minutes or as often as every minute.|
|Threshold	|If the user would like to receive alerts after a specific number of occurrences of the alert, set the number of occurrences as the threshold.|

# Subscribing to reports

<div class='ucc' />Administration > Users or Groups</div> 

To subscribe an account to reports, select the User ID associated with the user. Then from the left menu, select *Report Subscriptions*. This link is only active if the account is configured with an email address.

The report subscription specifies how often the report is created and emailed.

The report subscriptions link takes you to the *Report Subscriptions* page.
 
Choose the Local Manager inventory group or port from which to receive reports, and the file format for the report - CSV, HTML, or PDF. Click the Subscribe links to subscribe to the desired reports. Depending on the file format selected, the user may receive zipped files.

![Uplogix Control Center - Report Subscriptions](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-report-subscriptions-user.png) 

Session reports are available in the Principal Reports area at the bottom of the page. You can only subscribe to session reports on accounts that are configured as auditees on your user account. For more information on this, see Configuring the account to audit others and to be audited.