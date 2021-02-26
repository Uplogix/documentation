<!-- 5.4 -->
<div class='ucc' />Inventory</div>

# Overview

Use the Inventory tab to organize and manage Local Managers in groups.

![Uplogix Control Center](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-inventory.png)

* Most management operations occur at the group level.
* To view the group details, click the group name and the group detail page displays.
	* All functions concerning inventory groups can be accessed from the group detail page.
	* A gray icon indicates the group is empty.
* Inventory groups are always visible regardless of your privilege settings.

Defining and applying user roles, rules, and tasks across large numbers of Local Managers in physically separate locations, reduces the need to repeat the same operations on each unit and the risk of introducing the variations that can occur during manual operations.

By grouping Local Managers, all members of any inventory group can be treated the same while each inventory group can be treated differently. Many of the tasks that the Control Center manages, such as assigning user roles and defining rules, can be performed at the root level or within any child group. All members of the inventory group and its child groups automatically inherit the newly created information.

By default, the server provides the **Your Company** root group, which can be renamed, and the **Unassigned Group**, which is not editable. Neither of these can be deleted.

New inventory groups can be created within the root group. These child groups may also be nested. Groups may be based on any criteria that help organize your deployment. Local Managers can be reassigned from one group to another at any time.

# About the Unassigned group

Executing the **config system management** command on a Local Manager places it under management by a Control Center. The Local Manager is then placed in the Unassigned group on the Control Center, unless you have already created a placeholder for it in another group.

Unlike other inventory groups, **the Unassigned group does not provide management capabilities**. To manage a Local Manager, it must be reassigned from Unassigned to another inventory group. 

The Unassigned group cannot be deleted or edited and Local Managers cannot be reassigned to it.

To place a Local Manager in the Unassigned group, remove it from another inventory group. At the next heartbeat, the Local Manager will appear in the Unassigned group.

# Editing an inventory group

<div class='ucc'>Inventory > Group</div>

![Uplogix Control Center - Inventory Group](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-group.png) 

The name and description of the root group and any inventory group you add can be edited. Changes to the name or description affect only the selected inventory group. Child groups or Local Managers within the inventory group are not affected.

Click *Edit* to modify the group name (required) and description (optional).

> Use only printing characters when completing text fields. Spaces are considered printing characters.â€ƒ

# Adding an inventory group

<div class='ucc' />Inventory > Group</div>

Groups can be added from the Inventory and Group Detail pages. An inventory group name cannot be duplicated at a different level or within a different parent group. Use only printing characters when completing text fields. Spaces are considered printing characters.

Adding groups requires a unique name and optionally, a description.

## Inventory 

![Uplogix Control Center - Inventory - Add Group](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-inventory-add-group.png)

The *Add Group* button in the top left of the Inventory screen is initially disabled. To enable it, select an inventory group from the list. Be sure not to click on the name of the group, but rather the row (i.e., slightly to the right of the group name).

## Group Detail

![Uplogix Control Center - Inventory Group](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-group.png)

You can add a group from a group detail page by clicking on the *Add* button under the *Child Group* section in the middle of the page.

![Uplogix Control Center - Inventory Group](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-group-children.png)

> Groups cannot be added to the Unassigned group.

# Reassigning an inventory group

<div class='ucc' />Inventory > Group</div>

All groups, with the exception of the root and Unassigned groups, can be moved to another parent. Reassignment includes all of the child groups and Local Managers assigned to the inventory group.

![Uplogix Control Center - Reassign Group](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-group-reassign.png)

Click the **Reassign** button to move the group to another parent.

![Uplogix Control Center - Reassign Group - Choose Parent](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-group-reassign-parent.png)

The **New Parent** list displays any available inventory groups. Only the current parent and Unassigned group are not shown. Select the new parent from the menu.

Click **Save**. The inventory list is automatically refreshed and displays the new location of the inventory group.

# Deleting an inventory group

<div class='ucc' />Inventory > Group</div>

An inventory group can be deleted from the Control Center using one of the following methods:

Click **Remove** to move all the child groups and Local Managers into the parent group prior to deletion. 

Click **Remove Including Children** to delete the group, its child groups, and all Local Managers in those groups. Deleted Local Managers return to the Unassigned group when they re-establish contact with the server at the next heartbeat.

<div class='danger' />There is no delete confirmation.</div>

# Adding a Local Manager manually

Local Managers are automatically placed in the Unassigned group once they have been configured and complete an initial heartbeat. However, a placeholder can be set up for the Local Manager beforehand, so the Local Manager is automatically added to the appropriate group when it contacts the server.

Local Managers can be added from the main Inventory screen as well as Group detail pages. 

From the Inventory screen, select a group's row (not the group name) and click the *Add Uplogix* button in the top left of the work area.

From a Group Detail page, click the *Add* button at the bottom of the *Appliance Children* section in the work area.

![Uplogix Control Center - Add Appliance](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-group-add-children.png)

![Uplogix Control Center - Create Uplogix](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-create-appliance.png)

From the *Create Uplogix* page, enter the serial number of the Local Manager and an optional description.

Click *Save* to add the Local Manager to the inventory.
 
> Use only printing characters when completing text fields. Spaces are considered printing characters.

# Reassigning a Local Manager

<div class='ucc'>Inventory > Local Manager Summary</div>

Local Managers can be reassigned from one group to another (for example, from the Unassigned group to the root group). 

![Uplogix Control Center - Reassign Button](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-reassign-button.png)

To reassign a Local Manager, select it from the Inventory list and click on the *Reassign* button. 

![Uplogix Control Center - Reassign Group - Choose Parent](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-group-reassign-parent.png)

Select a new parent group from the dropdown list and click *Save*.

> While there is no function for moving a Local Manager into the Unassigned group, this can be done by deleting the Local Manager. If it is still configured to use the Control Center, it will reconnect on the next heartbeat and will then be placed in the Unassigned group.

# Deleting a Local Manager

<div class='ucc'>Inventory > Local Manager Summary</div>

A Local Manager can be removed from the Inventory by clicking the *Remove* button from the Local Manager Summary page. If the Local Manager is still configured to use the Control Center, it will reappear in the Unassigned group.

![Uplogix Control Center - Remove Appliance](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-reassign-button.png)

To set the Local Manager to operate without management by the Control Center, log into the Local Manager and use the **config system management** command to set *Use Management Server* to *no*.