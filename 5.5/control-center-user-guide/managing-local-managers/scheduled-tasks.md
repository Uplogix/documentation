<!-- 5.4 -->

<div class='ucc' />Schedule</div>

# Overview

Tasks can be scheduled to run once or on a schedule. To schedule a task:

- Create a task filter or select an existing task filter
- Choose and schedule the task

A filter specifies the portion of the inventory that is affected by a scheduled task. 

For example, to define a task that clears the counters on all Cisco devices within a specific inventory group periodically, a filter is needed which specifies all Cisco devices within that group. Use this filter to schedule the Clear counters task.

Filters and filter options are limited to Local Managers and ports to which you have **config schedule** access.

Some scheduled tasks are available from the expanded Local Manager Summary pages. These tasks are scheduled only on the individual Local Manager; therefore a filter does not need to be selected.

This section covers:

- Setting up filters and scheduling tasks
- Tasks that can be scheduled
- Scheduling tasks on a single Local Manager
- Scheduling software upgrades on Local Managers

Access the Schedule page by clicking *Schedule* on the navigation bar.

# Creating a filter

<div class='ucc' />Schedule > Filters</div>

To create a new filter, select **Filters** from the contextual left navigation on the Schedule tab. 

![Uplogix Control Center - Schedule Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters.png)

Click *Add* to create a new filter, or click an existing filter to edit it.

![Uplogix Control Center - Schedule Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters-new.png)

Enter a name and a description for the filter. The name of the filter cannot be changed once it is created, though the filter can be deleted and recreated under a new name.
 	
> Use only printing characters when completing text fields. Spaces are considered printing characters.

Click *Save*.

![Uplogix Control Center - Schedule Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters-edit.png)

Add filter criteria as needed by choosing a criterion and then clicking Add to register your choice. Multiple criteria can be applied in each section.

Initially, each section of the filter editor displays a message indicating that nothing has been added to this section of the filter. Use the Label section to use the port labels that have been created, if any. 

Device makes, operating systems, group names, and labels are presented in drop-down lists. Local Managers and devices are presented in the Hostname picker dialog boxes.

In the following example, the root Inventory group has been selected and added under the *Inventory Groups* section.

![Uplogix Control Center - Schedule Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters-edit2.png)

Click *Preview* to see which Local Managers and devices are affected by the filter. When satisfied with the filter, click Done to save your changes. The Filter Manager page now lists the filter which can be previewed, edited, or deleted.

![Uplogix Control Center - Schedule Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-filters-list.png)

# Scheduling a task

<div class='ucc' />Schedule > Scheduled Tasks</div>

Once task filters have been defined, tasks can be scheduled from the Scheduled Tasks page. Select *Scheduled Tasks* from the contextual left navigation on the Schedule tab.

> By default, the only tasks shown on the Scheduled Tasks List are tasks that have not yet been completed. To see all tasks, expand the *Search* section and select *Include completed*.
 
![Uplogix Control Center - Scheduled Tasks](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-tasks-empty.png)

Available task filters are shown in the Filter list. Choose the appropriate filter from the list. If the filter is not listed, click Cancel and create a new filter (see the previous section).
 
![Uplogix Control Center - Scheduled Tasks - Filters](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-tasks-filter.png)

There are several types of tasks that can be scheduled. The tasks available depend on the device platform. For example, the Clear Counters action is not available for servers.

Select a filter and a task, and click *Next*.
 
Some tasks, such as Change Authentication, take more than one step to schedule. Others, such as Clear Counters, present only a scheduling page.

![Uplogix Control Center - Scheduled Tasks - Frequency](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-tasks-frequency.png)

The default starting date and time is the current date and time. Change the date and time if the task is not to be executed immediately.

Complete the required information on each page, and click *Save*.
 
The Scheduled Tasks list shows the new task.

![Uplogix Control Center - Scheduled Tasks](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-schedule-tasks-list.png)
 
* Click the description text to view the equipment affected by the task.
* Click *Hold* to postpone the task.
* Click *Resume* when ready to allow the task to proceed.
* Click *Cancel* if the task should not be executed.

## Tasks that can be scheduled

The list of tasks available depends on the filter. If the filter specifies managed devices by make, some tasks are unavailable.
 
|Task	|Purpose|
|:---|:---|
|Certify|	This is an Alcatel specific task that validates a configuration before deploying it.|
|Change Authentication	|Schedule an authentication change for a device, with the option to change the console login and password, the enable login and password, and on some devices failover credentials used when centralized authentication systems are unavailable.|
|Clear Counters	|Clear interface counters on a device. All interfaces counters are cleared. |
|Config Import	|Import Local Manager configuration settings. The file to be imported must exist in the File Archive prior to scheduling. For more information, see Uploading files from your computer to the File Archive.|
|Device Ping	|Schedule a ping task from a device attached to the Local Manager to a target destination.|
|Download	|This task is a step in the process of applying a file to a Local Manager or a managed device. To make the file available to the Local Manager, it must be downloaded from the Control Center to the Local Manager. Before downloading files to Local Managers, they may need to be uploaded to the Uplogix Control Center. See Uploading files from your computer to the File Archive. To download a file from the Control Center to Local Managers, choose the type of file and file status based on where the file should be saved. Then select a file to download from the File Archive.|
|Interface	|Interfaces can be set on, off, or cycled at a specified time. Choose the desired action and enter the name of the interface.|
|Monitor	|Schedule interface, ping, chassis, console, or log monitors to run, defaults to 30 seconds.|
|Power	|Devices can be powered on, off, or power cycled at a specified time. Choose the desired action and if applicable, enter the delay between powering off and on.|
|PPP	|Schedule the Local Manager to initiate Outband (out-of-band) communication.|
|Pull SFTP	|Pull various files from device to Local Manager port file system utilizing secure FTP.|
|Pull TFTP	|Pull various files from device to Local Manager port file system utilizing FTP.|
|Push Config	|Push a new configuration onto a device by specifying the type of file and version. These options refer to files located on the Local Manager, in the port's file archive. Also, specify whether the device should be rebooted after the new configuration is loaded.|
|Push OS	|As with configurations, operating system images can be pushed onto a device.|
|Push SFTP	|Push various files to device from Local Manager port file system utilizing secure FTP.|
|Push TFTP	|Push various files to device from Local Manager port file system utilizing FTP.|
| Reboot	|Schedule a device to reboot at a specified time.|
|Reboot All	|This is an Alcatel specific task.|
|Reboot Working	|This is an Alcatel specific task.|
|Restart	|Restart the Local Manager.|
|Restore	|This is an Alcatel specific task.|
|Show Tech	|Execute low-level debug collection command on the device and automatically save the output to the Local Manager.|
|Update	|Update the Local Manager software. The new software image must exist in the File Archive prior to scheduling.|

# Scheduling tasks on a single Local Manager

<div class='ucc' />Inventory > Local Manager Summary Page</div>

Schedule the following tasks for a specific Local Manager from the Local Manager's detail page.
  
![Uplogix Control Center - Local Manager - Schedule Task](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-local-manager-schedule-task.png)

|Task	|Purpose|
|:---|:---|
|Config Import	|Import a configuration file. The appropriate file must be present in the File Archive. See Uploading files from your computer to the File Archive.|
|PPP	|Schedule an Outband on, cycle, or off action.|
|Restart	|Restart the Local Manager.|
|SLV Monitor	|Setup SLV monitors. This task is available only if your license includes Service Level Verification. In addition, the appropriate SLV tests and rules must be available.<br><br>For detailed information about creating rules, refer to the Guide to Rules and Monitors.|
|SMS Message|	Send an SMS message to a Local Manager containing a command to execute. Only PPP on (Outband) is supported.|
|Update	|Schedule a software upgrade for the Local Manager. The appropriate file must be present in the File Archive; otherwise the update cannot be scheduled.|