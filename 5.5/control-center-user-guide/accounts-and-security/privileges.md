<!-- 5.4 -->

# Overview

Permissions, roles, and privileges are defined as follows:

* **Permission** - Ability to use a specific command or capability; can be allowed or denied in a role definition
* **Role** - A named set of permissions that a user is permitted to execute, such as admin
* **Privilege** - A role assigned to a specific account for a specific resource, such as "admin on system" or "guest on port 1/4"

> Some permissions, such as **config hierarchy**, are not associated with specific commands but provide override ability and should be used sparingly.

The Control Center restricts access to features based on a user's privileges. For example, if a user does not have a role that includes permission to use the **config system ip** command, the IP configuration link is unavailable for that user on the Local Manager Summary page.

All aspects of working with the Control Center and the equipment it manages are affected by account privileges. **By default, user and group accounts have no privileges.**

The *administrator* account on the Control Center has admin (role) access to all features of the server, but no privileges on individual Local Managers. Administrator cannot log into a Local Manager. Conversely, the admin (user) account on Local Managers has no privileges on the Control Center. However, the administrator account has the **config hierarchy** permission, which allows the administrator to manage individual Local Managers through the Control Center.

In this section:

- Adding server privileges to accounts
- Adding inventory privileges to accounts
- Viewing and deleting user account privileges
- Creating and customizing roles
- Using TACACS to manage privileges
- Creating a superuser
- Limiting a user's access to one port on one system

# Adding Server Privileges to Accounts

<div class='ucc' />Administration > Server Privileges</div>

When a new user or group account is created, the account has no privileges. To log into the Control Center and work with its web interface, users must have appropriate levels of server privileges.

Privileges on the Control Center are assigned separately from privileges on the equipment in the inventory. Both are needed if a user is to use the Uplogix web interface to work with Local Managers and to access Local Managers individually via SSH. 

To assign server privileges, go to the Server Privileges page on the Administration tab.
 
![](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-server-privileges.png)

Unlike Inventory privileges, server privileges only apply to one resource - the Control Center.

Select a user or group from the User/Group list, select a role, and click *Add*. Groups are listed first, followed by users. An * after the group name indicates a group.

As with Local Manager privileges, more than one role can be assigned to an account to tailor that account's privileges.

# Adding Inventory Privileges to Accounts

<div class='ucc' />Inventory > Group Detail > Security > Privileges</div>

When a new user or group account is created, the account has no privileges. Set an account's privileges to apply to all Local Managers in the inventory by assigning them at the root level or limit privileges to specific inventory groups.

To add Inventory privileges, select the appropriate Inventory group from the Inventory page and click *Privileges* under the Security menu.

![Uplogix Control Center - Group Privileges](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-group-privileges.png)

Use the Privilege page to assign privileges to accounts in the form of defined roles and to specify the resources where each role is applied: all, system, or modem. If labels have been created, these are available as resources also.

Select a user or group from the *Principal* list, select a role, and click *Add*. Groups are listed first, followed by users. An * after the group name indicates a group.

More than one role can be assigned to an account and be given different roles on different resources.
 
To remove privileges at the port level, select a Local Manager from the inventory and select Privileges from Security menu.

Use the Local Manager's  Privilege List to add or delete user roles by individual resource. If the pre-configured standard roles do not meet your organization's needs, create roles to meet the specific requirements of your deployment. See Creating and customizing roles.

# Viewing and Deleting User Privileges

<div class='ucc' />Administration > Users</div>

To view or edit a user's privileges, click the *User ID** and then select *Privileges* from the left menu.

Use the *Privileges* page to see and delete specific privileges.

# Creating and Customizing Roles

<div class='ucc' />Inventory > Inventory Group > Security > Roles</div>

A role is a set of commands that a user is permitted to execute. When privileges are assigned to a user or group account, the account is associated with one or more roles on one or more resources. See Adding inventory privileges to accounts.

The Control Center provides the same predefined roles that are available in the Uplogix LMS CLI. In addition to these standard roles, custom roles can be defined to suit your deployment. Roles may be created at the root level to apply globally or they may be created within an inventory group to apply only to that group and its child groups.

To view a list of roles defined for any given inventory group, select the group from the inventory list and click *Roles* under the Security menu.

On the *Roles* page, click *Add* to add a role or select the role's name to edit an existing role. This is equivalent to issuing the **config role** command from the command line.
 
![Uplogix Control Center - Create Role](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-create-role.png)

The role name is required when creating a new role.

> Use only printing characters when completing text fields. Spaces are considered printing characters, but may only be used in the description field.

Specify the role permissions by selecting them from the Available Permissions list and using the *Add Allow* and *Add Deny* buttons.

To select more than one permission at a time, use shift-click on the first and last items in a range or use control-click to select permissions separately.
 
As with other settings, when a role is created it is automatically inherited by any Local Managers and child groups within the current inventory group. If a role with the same name already exists on a Local Manager or child group within the current inventory group, select *Force update on children* to overwrite it.

Once the privileges for the role are defined, click *Save*.

# Example: Creating a Superuser

The Control Center is a resource, just as Local Managers and their ports, modems, and power controllers are resources. Users cannot log into the Control Center until they have privileges. 

To create a superuser:

1. Create the user under *Administration -> Users*
2. Give the user the admin role on the server resource under *Administration -> Server Privileges*
3. Give the user the admin role on all resources on the root Inventory group under *Inventory -> Group -> Security -> Privileges*

The user now has access to all commands and capabilities on the Control Center and on all equipment at every level of the inventory.