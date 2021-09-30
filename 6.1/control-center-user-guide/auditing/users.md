<!-- 5.4 -->

# Overview

<div class='ucc' />Administration > Users > User Name > Auditing</div>

To audit users, your account configuration must include:

- A valid email address
- The permission to audit the user as one of your auditees
- A report subscription to the appropriate session report on each user to be audited. 

The reports are emailed as PDF, HTML, or CSV files.

The following example shows how to configure a user to audit another user. In this example, the user *super* (who has the admin role on the Control Center) will be configured to audit another user, *jsmith*.

Every user account is automatically able to audit itself. To audit others, auditees must be added to the auditor's user profile.

From the Auditing menu, click *Add* under Auditees.

![Uplogix Control Center - Auditing](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-auditing.png)
 
From the pop-up, select the user to be audited, in this case, *jsmith* and click *Add Auditee(s)*.  Click *Save* at the top or bottom of the page and the auditees are added to the auditee listing.

![Uplogix Control Center - Add Auditee](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-add-auditee.png)

> You must click *Save* after adding the auditee, even though the page appears to have refreshed. We're working on that.

The *super* account has an email address, and the user *jsmith* is now among *super's* auditees, so *super* will be able to subscribe to reports on *jsmith*.

The next step is to subscribe to the desired reports. Click *Report Subscriptions* from the left menu to go to the Report Subscriptions page. 

On the Report Subscriptions page, expand the *Principal Reports* section at the bottom of the Report Subscriptions page.

Select the Principal (the user to be audited). If your account is configured to audit many users, you may wish to enter a filter string to shorten the list of usernames.

![Uplogix Control Center - Report Subscriptions](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-report-subscriptions-audit.png)
 
Select the auditor's email address if more than one is available, and choose the file type that will be emailed (PDF, HTML, or CSV). Then *Subscribe* to the desired report. 

- Activity reports&mdash;include all page views.
- Change reports&mdash;include all actions that resulted in changes on the Control Center, any Local Manager under management, or any device connected to a managed Local Manager.
- Full reports&mdash;include all information from both activity and change reports.

Use the radio buttons next to the reports to select which reports to receive and click on the *Subscribe* button.  The new subscription is listed at the top of the Report Subscriptions page, and in the Report Subscriptions area of the Edit User page.