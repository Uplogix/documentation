<!-- 5.4 -->

<div class='ucc'>Administration > Users</div>

# Overview

Use the Users and Groups pages under the Administration tab to manage accounts. The options on the Create/Edit User and Create/Edit Group pages are the same as those found in the CLI commands **config user** and **config group**.
 
![Uplogix Control Center - Users](http://uplogix.com/support/docs/img/6.0/users-list.png)

Accounts that exist locally on a Local Manager are deleted when the Local Manager makes contact and synchronizes with the Control Center. Accounts cannot be managed locally through the command line if the Local Manager is managed by a Control Center.

There is an exception for users whose passwords expire. If you log into a Local Manager with an expired password, the command line prompts for a new password. When you set the password, it is pushed up to the Control Center.

# Creating and Editing Users

<div class='ucc'>Administration > Users</div>

To add a new account, click *Add*.

To edit an existing user account, click the *User ID*. When an existing user is edited, the *Edit User* page displays a timestamp showing when the account was created. The account name cannot be edited.

Search the list of users by entering a text string in the search box, select the type of search, and click *Search*.
 
Complete the fields needed to create the account and set it up appropriately for your environment.

> Account names must be unique. For example, if there is a group account called *sysadmin*, a user account called *sysadmin* cannot be created.

> Use only printing characters when completing text fields. Spaces are considered printing characters, but may only be used in the description field.

> Do not create a password that ends with a space character. When an attempt to log into a Local Manager is made using a password that ends with a space, the Local Manager strips the space character and the login fails.

![Uplogix Control Center - Users](http://uplogix.com/support/docs/img/6.0/create-user.png)

> If the Time Zone setting for a user account is changed while that user is logged in to a Local Manager, the change does not take effect on that Local Manager until the user ends the session.

Click *Save* when finished setting up the account information.

Initially, user accounts have no privileges, so the new user cannot log into the Control Center or to the Local Managers within the deployment. Privileges must be assigned to the new user account to allow the user to work with elements of your deployment. See Managing privileges.

Some users may need to receive alerts, reports, or audit other accounts. For information about setting up these functions, see Setting up email, auditing and report subscriptions.

Several users can be created at once by importing a user file. See [Importing User, Groups, and Privileges](http://uplogix.com/docs/control-center-user-guide/accounts-and-security/importing-aaa).
â€ƒ
# Creating and Editing Groups

<div class='ucc' />Administration > Groups</div>

Use the Control Center to create and manage group accounts across multiple Local Managers to ensure a consistent user group organization and privilege policy.

To create or edit a group account, select Groups from the left menu under the Administration tab. Existing groups are displayed in the Group box.

![Uplogix Control Center - Groups](http://uplogix.com/support/docs/img/6.0/groups-list.png) 

To create a new group, click *Add*. Specify a name for the group and optionally provide a description as well as a start and expiration date.

![Uplogix Control Center - Create Group](http://uplogix.com/support/docs/img/6.0/create-group.png)

To edit an existing group, click the *Group ID*. This is equivalent to issuing the **config group** command from the Local Manager command line. When an existing group is edited, the *Edit Group* page displays a timestamp showing when the account was created.

> Account names must be unique. For example, if there is a user account called sysadmin, a group account called sysadmin cannot be created.

> Use only printing characters when completing text fields. Spaces are considered printing characters, but may only be used in the description field.

Once the group is created, add users or other groups as members of this group. Members of the group inherit group-related settings such as privileges.

![Uplogix Control Center - Users Added to Group](http://uplogix.com/support/docs/img/6.0/edit-group.png)
 
The Available Users and Available Groups list are populated with information from the Control Center database. To add a new member to a group, the new user or group must first exist in the database. Click *Add* and select the user or group from the pop-up window as appropriate.

Click *Save* to save the group. Initially, user groups are automatically inherited by Local Managers. Initially, group accounts have no privileges, so members of the group have only the permissions assigned to their individual accounts. Group privileges must be assigned to the new user account to allow the user to work with elements of your deployment.

The group may need to receive alerts, reports, or audit other accounts. For information about setting up these functions, see [Auditing](http://uplogix.com/docs/control-center-user-guide/auditing/) for more information.

Several groups can be created at once by importing a group file. See [Importing Users, Groups, and Privileges](http://uplogix.com/docs/control-center-user-guide/accounts-and-security/importing-aaa).
â€ƒ
# Disabling Users

<div class='ucc' />Administration > Users</div>

To suspend access to a user account without deleting the account, select the User ID of the account and check the *Disabled* box. Click *Save* to save your changes.

The user is not able to log in while the account is disabled. The status of Disabled displays in the user list. 

If the user is logged in when their account is disabled, the user is logged out immediately.

# Deleting Users and Groups

To delete a user or group, click the check box associated with the User ID or Group ID and select Remove. This is equivalent to using the LMS commands **config user no [username]** and **config group no [groupname]** on a Local Manager not managed by a Control Center.

<div class='danger' />There is no delete confirmation.</div>