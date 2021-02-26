<!-- 5.4 -->

# Overview

The Control Center regularly archives data received from Local Managers. Reports can be generated from the inventory group and Local Manager level. A report from the inventory group level includes information from all Local Managers within the inventory group, while the Local Manager level only includes the specific Local Manager.

#Inventory Group Reports

<div class='ucc' />Inventory > Group Detail > Reports</div>

Access inventory group reports from the Group Detail page. Expand the *Reports* menu and click the link for the report of interest.

![Uplogix Control Center - Reports](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-reports.png)
  
If necessary, specify the desired range of times.

Reports start at the beginning of the specified time span. For example, a weekly report begins on Sunday rather than showing the previous seven days; a monthly report begins on the first of the month rather than showing the previous 30 days.

![Uplogix Control Center - View Report](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-view-report.png)

Once the time period of interest is specified, click *Display*, *Download PDF* or *Download CSV* as appropriate.
â€ƒ
# Local Manager Reports

<div class='ucc' />Inventory > Local Manager Summary > Report</div>

Access Local Manager specific reports from the reports menu on the Local Manager page.

# Reports by Label

<div class='ucc' />Reports > Reports by Label</div>

Most reports are available on the Group Detail, Local Manager Summary, and Port Detail pages. However, reports can also be generated for custom labels. If labels have been created for managed devices, standard reports for each label are available on the Reports by Label page.

![](http://uplogix.com/support/docs/img/cc-user-guide/image135.png)
â€ƒ
# Report Files

<div class='ucc' />Reports > Report Files</div>

Reports are generated from Jasper XML files. Several are included with the Control Center, but custom files can also be uploaded. Once uploaded, these files are available for use on the Report Assignments page.

After creating a custom Jasper file, browse to find it and click upload. The file is now available from the list of files on the Report Assignments page.
 
![](http://uplogix.com/support/docs/img/6.0/ucc-custom-report-files.png)

Please contact [support@uplogix.com](mailto:support@uplogix.com) if you need assistance with this feature.

# Report Assignments

<div class='ucc' />Reports > Report Assignments</div>

The Control Center can generate a wide range of reports on a variety of subjects. These correspond to the reports listing seen on the Group Detail, Local Manager Summary, and Port Detail pages. 

Reports are generated in various formats and emailed to system users or groups.

Use the Report Assignments page to schedule any of the existing reports.
 
To create a new report assignment: 

- Choose the **scope**â€”this may be label, inventory group, system, or port.
- Choose a **group**â€”this may be alarms, changes, events, logins, custom, or none.
- If there is at least one report in the group chosen within the selected scope (for example, alarm reports on inventory group pages), select the **offset**. This specifies the report's position in the list. An offset of 0 places the report first on the list.
- Name the report, select the appropriate jrxml format file, and choose the frequency of report generation.
In the following example, a weekly report of GPS events on managed devices is created. The report is available from inventory group pages under a custom report grouping.
 
![](http://uplogix.com/support/docs/img/6.0/ucc-create-report-assignment.png)

Click *Assign* to create the report and assign it to the specified scope. In this example, the report is assigned to inventory group pages. The report is now available.

![Uplogix Control Center - Custom Label Report](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-reports-files.png)

Although an existing report assignment cannot be edited, a new report assignment with the same name can be created. This overwrites the existing report assignment.
