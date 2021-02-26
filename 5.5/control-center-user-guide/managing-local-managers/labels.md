<!-- 5.4 -->

# Overview

<div class='ucc' />Inventory > Local Manager > Port > Labels</div>

There are several methods to manage your Uplogix deployment and managed devices. Use inventory groups to manage Local Managers by logical groups such as location or business unit. Device information entered during port configuration of the Local Managers allows users to manage devices by make and model. Finally, users can assign labels to a Local Manager's managed devices to group them in more flexible ways.

Labels can be used to group devices by other criterion such as maintenance windows, scheduling reports, or assigning privileges on all routers regardless of make. Another would be grouping managed devices by business unit in cases where several business units share a Local Manager.

Labels are managed from the Control Center and cannot be assigned from the Local Manager's LMS command line.

# Creating port labels

<div class='ucc' />Inventory > Local Manager > Port > Labels</div>

To assign a label to a port, select a Local Manager, a port, and then *Labels* from the menu on the left.

![](http://uplogix.com/support/docs/img/ucc5.2/labels_add.png)

Click the **Labels** menu item to open the Labels page.

Create a new label for the port and then click **Add** to apply the label to this port. More than one label can be applied to a port.

# Assigning privileges by label

<div class='ucc' />Inventory > Group > Security > Privileges </div>

Privileges are created by assigning the user or user group a role (such as admin or guest) to a resource (such as port 1/2). The default resources within the inventory are the same resources found in the Local Manger command line interface - system, modem, and the individual ports. If labels have been created, they are also considered resources.

The example below shows how to assign admin rights to a user on all routers. For more information about assigning privileges, see Managing privileges.

![](http://uplogix.com/support/docs/img/ucc5.2/labels_privileges.png)

# Setting up task filters using labels

<div class='ucc' />Schedule > Filters</div>

Use Labels as a filtering criterion when setting up filters for scheduling tasks. View and edit these filters on the Schedule > Filters page. For more information about task filters, see Setting up filters and scheduling tasks.
 
![](http://uplogix.com/support/docs/img/cc-user-guide/image060.png)

# Viewing reports by label

<div class='ucc' />Reports > Reports by Label</div>

Once labels are assigned to port devices, the Control Center automatically creates reports based on the labels. View these reports on the Reports > Reports by Label page. For more information about reports, see Viewing reports.

![](http://uplogix.com/support/docs/img/cc-user-guide/image061.png)