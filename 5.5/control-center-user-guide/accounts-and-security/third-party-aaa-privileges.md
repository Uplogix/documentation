<!-- 5.4 -->
# Overview

Setting up a user account to use a RADIUS or TACACS ACL allows the TACACS server to send group member information in the initial login transaction. To use this feature, the account must be set up on the RADIUS/TACACS server. 

The general procedure is as follows:

1.	Configure the Control Center to use RADIUS or TACACS.
2.	Set up a user group and associate a RADIUS or TACACS ACL to it.
3.	Assign at least one role to give the group the desired set of permissions; create a suitable role if necessary.
	
These steps are described in detail below.

> If AAA functions are delegated to an external server, create a user with the admin role on the Control Center and add that account on the external server beforehand. If no user has the admin role on the Control Center, the administration functions are not accessible.

# Set up Authentication

On the *Administration > AAA Settings* page, set up the Authentication Settings as follows:

1)	Under *Authentication Type*, select *RADIUS* or *TACACS*.
2)	Select the appropriate authentication method.
3)	Select *Use RADIUS/TACACS Authorization*.
4)	If you want to automatically create Uplogix user accounts for users found in your AAA server, choose Select *Create Users*. 
5)	Enter the IP address and shared secret for each AAA server. Up to four servers may be specified.
6)	Optionally, select *Cache Passwords* to ensure that user accounts, passwords and privileges will still be available if the AAA server is offline during a future login authentication/authorization.
 
![](http://uplogix.com/support/docs/img/cc-user-guide/image112.png)
â€ƒ
When a user logs in to the Control Center with Cache Passwords enabled, the Control Center verifies the password with the authentication server and then updates the user account (caching) on the Control Center. Since the account is updated, this change gets pushed down to all the Local Managers, changing the user's password on Local Managers throughout the inventory.

Using this method, the Control Center can be configured to use AAA, but the Local Managers don't have to. The Local Manager receives the user's new password via the Control Center and authenticates locally with the password received remotely. Although the user logs into the Local Manager with the account's TACACS password, the Local Manager is not really contacting the TACACS server.

In this scenario, if the user's password changes on TACACS, it is not updated on the Local Managers in the inventory until the user logs into the Control Center to cache the new password. At this time it is pushed to the Local Managers. Evaluate whether this is a suitable approach for your environment.

> Uplogix User passwords are encrypted on the Control Center and Local Manager using AES encryption.

# Create a Group

The group provides a means to associate roles to the TACACS ACL. The name of the group should match the TACACS ACL exactly.

Under *Administration > Groups* create a group with the same named as the TACACS ACL to be returned.

Assign suitable roles to the group. Users are not able to log in until they have roles.

# Enable Authorization on an Existing TACACS User

Once the user is created and is able to authenticate to the Local Manager, authorization can be added by adding an ACL under the â€œExecâ€ service in your user or group. In most Unix TACACS deployments, the users file can be edited and the following lines can be added to either the group or the user:

```
service = exec {
acl = <acl name/number from Uplogix Control Center group>
}
```

Refer to your TACACS administrator guide for more specific examples of configuration required for this functionality.

# Enabling Authorization on a TACACS User with Cisco ACS

To enable authorization on an existing TACACS user with Cisco ACS:
1.	On your ACS, create a group for your users and then edit it by clicking Edit Settings.
2.	Edit this group to include the following options: Shell (exec) and Access control list.
3.	Add a list of groups that you wish your users to be a part of, and then click **Submit + Restart**.

##Associate the ACL to users on the RADIUS Server

Create new users or add the ACL to existing users.

- The RADIUS Vendor specific attribute (VSA) "Uplogix-Version" is used to configure information specific to Uplogix.
- A new field called "Uplogix-User-Groups" in the VSA to hold a user's group information should be created.
 - The field can contain a single group name or comma-separated list of groups.
 - The group names must be established and configured on the Uplogix system separately from the RADIUS configuration.
 - On successful login on RADIUS, the VSA for Uplogix will be returned with the RADIUS response to the Uplogix device.

These steps are described in detail below.

- The Radius Dictionary contains these fields and is also available from the Uplogix support site.

|||||
|:---|:---|:---|:---|:---|
|Uplogix			|10243|||
|BEGIN VENDOR	|Uplogix|||
|ATTRIBUTE		|Uplogix |Version			|1	|string|
|ATTRIBUTE		|Uplogix |User Groups		|3	|string|
|ATTRIBUTE		|Uplogix |CLI Command		|4	|string|
|ATTRIBUTE		|Uplogix |Envoy Serial		|5	|string|
|ATTRIBUTE		|Uplogix |Task ID			|6	|string|
|END VENDOR		|Uplogix|||

Or in plain text format:

```
Uplogix	10243
BEGIN VENDOR	Uplogix
ATTRIBUTE	Uplogix	Version	1	string
ATTRIBUTE	Uplogix	User Groups	3	string
ATTRIBUTE	Uplogix	CLI Command	4	string
ATTRIBUTE	Uplogix	Envoy Serial	5	string
ATTRIBUTE	Uplogix	Task ID	6	string
END VENDOR	Uplogix
```