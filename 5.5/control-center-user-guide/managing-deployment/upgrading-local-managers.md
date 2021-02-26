<!-- 5.5 -->

# Overview

Local Managers can be upgraded individually (e.g., when adding a new unit to the deployment), both from the UCC and CLI, or you can schedule them to upgrade in batches (e.g., after a Control Center upgrade.)

Here are some best practices to consider:

* To ensure availability of the Control Center's web interface, upgrade no more than 100 Local Managers simultaneously.
* Schedule an upgrade for all Local Managers and let it run. Investigate the Local Managers that don't upgrade for network or system issues.

The information presented in this article is a subset of [Managing Scheduled Tasks](http://uplogix.com/docs/control-center-user-guide/managing-local-managers/scheduled-tasks).

# Uploading New Software

<div class='ucc' />Administration -> File Archive</div>

Before you can schedule an update task, you need to upload the new Local Manager software (.bin file) to the Control Center's File Archive.

Access your Control Center, click on the Administration tab, and choose File Archive on the left side of the page.

![Uplogix Control Center - File Archive Blank](http://uplogix.com/support/docs/img/uplogix-control-center-file-archive2.png)
 
If you do not already have a category defined, enter a new name (e.g., "LMS_Software"). Click Choose File to locate the upgrade file on your computer. Add an optional description and click Upload.

> File Archive category names cannot contain spaces or special characters.

![Uplogix Control Center - File Archive Upload](http://uplogix.com/support/docs/img/Untitled-3uplogix-control-center-file-archive-upload3.png)

If you are using a recent version of Google Chrome, the upload percentage will appear in the lower left of the browser window.

Once the file upload completes, it will be listed in the File Archive.

![Uplogix Control Center - File Archive List](http://uplogix.com/support/docs/img/uplogix-control-center-file-archive-list2.png)

# Creating a Filter

<div class='ucc' />Schedule > Filters</div>

When scheduling tasks for multiple Local Managers, you must create a filter that specifies which Local Managers will be affected. The Filters page is located under the Schedule tab.

![Uplogix Control Center - Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters.png) 

Customers with less than 100 Local Managers may want to create a filter that applies to all systems. Those with larger deployments may want to break up their filters into geographic regions or simply groups of one hundred. The process is the same.

Click *Add* to create a new filter. Enter a filter name and optional description and click *Save*.

The filter will be created and you will be taken to the Edit Filter page.

![Uplogix Control Center - Edit Filter](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters-edit.png)

To create a simple filter that applies to all Local Managers, select your root inventory group under the Inventory Groups section and click *Add*.

![Uplogix Control Center - Edit Filter](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters-edit2.png)

Adding the root inventory group means the filter to apply to all Local Managers in the root group or any child groups.

Click *Done* to exit the filter editor.

# Scheduling the Update Task

Click on Scheduled Tasks on the left side of the page.

![Uplogix Control Center - Scheduled Tasks](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-tasks-empty.png)
 
Click Schedule Task.

![Uplogix Control Center - Select Filter](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-tasks-filter.png)

Select the filter against which the task will be scheduled. In our example, it is the "All Local Managers" filter we just created.

Select the *Update* task from the dropdown menu.

Click *Next* on the right side of the page.

Since we selected the Update task, we'll need to specify an update file.

![Uplogix Control Center](http://uplogix.com/support/docs/img/uplogix-control-center-schedule-tasks-update2.png)

Select the update file from the list and click Next.

> While *Ignore Data Loss* warning may sound ominous, it is only applicable when downgrading software on a Local Manager as most data cannot be retained.

![Uplogix Control Center - Task Frequency](http://uplogix.com/support/docs/img/uplogix-control-center-schedule-tasks-frequency2.png)

Update tasks can be run immediately (default) or at a scheduled time. When this page is initially loaded, the current time is populated as the Start time. Do not modify the Stop or Repeat options, as we only want the upgrade to run once.

If you wish to run the update at a later time, modify the Start time. Otherwise, click Save.

# Checking Task Status

With the task scheduled, head over to the Inventory page and expand your groups. Because the Inventory page auto-refreshes, you can watch the progress of your upgrade through the status icons of the Local Managers.

Initially, the Local Managers may show a yellow icon, indicating they are communicating in Minimal Heartbeat mode, which is expected for Local Managers on a lower revision of code.

Once they download the software, unpack it, verify it, and restart, their status icons will turn gray and may remain that way for 10-15 minutes.

Once the upgrade is complete and normal heartbeat resumes, the status icon will return to green.