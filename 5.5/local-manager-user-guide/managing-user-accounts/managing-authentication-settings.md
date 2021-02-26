<!-- 5.4 -->

This section provides information about Authentication, Authorization, and Auditing when using a third-party AAA server.

If you are not using a third-party AAA server, AAA is handled by local user accounts, the built-in roles system, and session logging.

# Authentication and Accounting

For security, individual users should be assigned unique usernames, passwords, and authority. Accounting and user authentication may be managed locally on the Local Manager, centrally on the Control Center, or remotely on an external RADIUS or TACACS server.

With the exception of the admin user, all local users are deleted when a Local Manager is placed under management of a Control Center. Maintain the admin user's local modifications, if any exist, using the AAA settings on the server. Users and groups on the server are globally unique and are applied to all Local Managers.

TACACS and RADIUS servers can be used for authentication, authorization and accounting.

The settings in this section can be configured with the interactive **config system authentication** command. Most of the settings are only displayed if the *Authentication Type* is set to TACACS or RADIUS.

## Authentication type

Available options are *local*, *tacacs*, and *radius*. These are case-sensitive. Some of the command prompts depend on the authentication type you specify.

## Limit maximum concurrent sessions

Sessions can be limited to one per login or to any number you specify.

## Authentication method

Supported authentication methods include PAP, CHAP, and MS-CHAP.

## Accounting type

The auditing feature can send executed commands to an accounting server. Choose *start-stop* to send audits before and after each command, *stop-only* to send audits only after commands, or *none* for no auditing.

> RADIUS accounting can only be used with RADIUS authentication and TACACS accounting can only be used with TACACS authentication.

## Use RADIUS/TACACS authorization

The local permission scheme can be overridden by using RADIUS or TACACS as an authorization source respectively.

See [Using Third-Party AAA to Manage Privileges](http://uplogix.com/docs/control-center-user-guide/accounts-and-security/third-party-aaa-privileges) for more information.

## Create users

If a user successfully authenticates with an external authentication source, but does not exist on the Local Manager, a user account can be automatically created. This option is disabled by default.

> This setting is only displayed if *Use RADIUS/TACACS authorization* is enabled.

## Cache passwords

The Local Manager can be configured to save passwords if the user authenticates successfully with an external server. The password is written to their user account and synchronized throughout the deployment.

This feature can be used in conjunction with *If server is down, should the system use local authentication* to provide failover protection in case of a network outage.

## If server is down, should the system use local authentication

The Local Manager can fall back to local authentication if it cannot contact the authentication server. If *Cache Passwords* is enabled, users will be able to log in with their RADIUS or TACACS passwords, provided their passwords were cached during a previous login. If *Cache Passwords* is not enabled, a local, secondary password can be added to user accounts for use during a network outage.

## Authentication Servers

Enter the IP address, port, and shared secret of up to 4 authentication servers.

> The default port for TACACS is 49, while the default port for RADIUS is 1812.

Successful authentication requires an affirmative response from one of the configured servers. If a server fails to respond, the next server is queried. An unresponsive server is not treated as a failed authentication; however, if a server responds and fails the authentication, the user will be denied access.

## Accounting Severs

This option is displayed if *Account Type* is set to *start-stop* or *stop-only*.

Enter the IP address, port, and shared secret of up to 4 accounting servers.

## Use strong passwords

To enhance security, you can require users to choose strong passwords based on restrictions you specify:

```
Use strong passwords: (y/n) [n]: y
     Require mixed case: (y/n) [n]: 
     Require numbers and punctuation: (y/n) [n]: 
     Reject variation of login id: (y/n) [n]: 
     Reject word in dictionary: (y/n) [n]: y
          Reject standard substitutions (@ for a, 3 for e, etc): (y/n) [n]: 
     Reject sequences in numbers or letters (qwerty): (y/n) [n]: y
     Reject previous password: (y/n) [n]: y
          Number of previous passwords to check [1 to 20]: [6]: 6
     Reject single character difference from previous password: (y/n) [n]: y
     Enforce minimum password length: (y/n) [n]: y
          Minimum password length: [6]: 8
```

**Require mixed case** â€” password must have both capital and lowercase characters. Valid password example: PassWord

**Require numbers and punctuation** â€” password must include at least one numeral and at least one symbol. Valid password example: P@ssW0rd

**Reject variation of login id** â€” password must not be a simple variation of the login id

**Reject word in dictionary and reject standard substitutions (@ for a, 3 for e, etc.)** â€” if both are selected, users may not set passwords such as p@$$w0rd. Valid password example: P&ssW*r#

**Reject sequences in numbers or letters** â€” users may not set passwords that consist of all the letters or numbers on one row of the keyboard, in sequence either from left to right or right to left, or a character string that contains such a sequence. Broken sequences such as abc!defg or qwerty12 may be used.

**Reject previous password and number of previous passwords to check** â€” obvious variations on the previous password will be rejected. The following examples assume that the previous password was P@ssW0rd.

* change of case only; p@SSw0rD will be rejected
* reversed character sequence; dr0Wss@P will be rejected
* doubled sequence; P@ssW0rdP@ssW0rd will be rejected
* string containing the earlier password; myP@ssW0rd! will be rejected

**Reject single character difference from previous password** â€” when changing a password, at least two characters must be changed.

Once strong passwords are implemented, failed login attempts will extend the time between retries to defer dictionary attacks.

**Expire password**

You can specify a time limit for passwords and have them expire automatically. If a user logs in using an expired password, the Local Manager allows the login and immediately prompts the user to set a new password.

**Number of invalid attempts before lockout**

Enable lockout by specifying the maximum number of times a user can attempt authentication before the Local Manager refuses further attempts. Setting lockout to 0 disables lockout protection. If lockout is enabled, the Local Manager prompts to specify the number of minutes the user will be locked out. The default lockout time is 30 minutes.

# Using TACACS/RADIUS to manage privileges

Setting up the Local Manager to delegate group membership to a TACACS ACL or RADIUS Group allows the server to manage Uplogix authorization. Groups are assigned permissions to resources and group members are added when the attribute is sent in the RADIUS or TACACS authentication response. To use this feature, set up the group on the Local Manager and on the TACACS server.

> If AAA functions are delegated to an external server, create a user with the admin role on the Local Manager and add that account on the external server beforehand. If no user has the admin role on the Local Manager, the administration functions are not accessible.

The steps below will set up TACACS/RADIUS authentication for a single Local Manager. To set up TACACS/RADIUS for the entire deployment, see [Using Third-Party AAA to Manage Privileges](http://uplogix.com/docs/control-center-user-guide/accounts-and-security/third-party-aaa-privileges).

## Set up TACACS authorization

Configure authorization using the **config system authentication** command. Make the following changes:

* Set authentication type as tacacs.
* For authentication method, enter pap, chap, or ms-chap, as appropriate.
* Answer y to the Use TACACS Authorization prompt.
* Usernames and attributes created on the Local Manager or UCC will be added to the specific groups for the userâ€™s session duration. If users are not defined in the Local Manager beforehand a successful authentication can create the account. Answer y to the Create users prompt.
* Optionally, answer y to the Cache Passwords prompt to persist TACACS created usernames and group membership. This will ensure that users will still receive the correct privileges if the TACACS server is offline during the next authentication/authorization.
* Enter the IP address, port, and shared secret for each TACACS server. You may specify up to four servers.

```
[admin@UplogixLM]# config system authentication
--- Existing Values ---
(output removed)
--- Enter New Values ---
Authentication type: [local]: tacacs
Authentication method: [pap]:
Accounting type: [none]: 
Use RADIUS/TACACS Authorization: (y/n) [n]: y
Create users: (y/n) [n]: y
Cache passwords: (y/n) [n]: y
If server is down, should the system use local authentication: (y/n) [n]: y
(output removed)
```

## Set up RADIUS authorization

Configure authorization using the **config system authentication** command. Make the following changes:

* Set authentication type as radius.
* For authentication method, enter pap, chap, or ms-chap, as appropriate.
* Answer y to the Use RADIUS Authorization prompt.
* Usernames and attributes created on the Local Manager or UCC will be added to the specific groups for the userâ€™s session duration. If users are not defined in the Local Manager beforehand a successful authentication can create the account. Answer y to the Create users prompt.
* Optionally, answer y to the Cache passwords prompt to persist RADIUS created usernames and group membership. This will ensure that users will still receive the correct privileges if the RADIUS server is offline during the next authentication/authorization.
* Enter the IP address, port, and shared secret for each RADIUS server. You may specify up to four servers.

```
[admin@UplogixLM]# config system authentication
--- Existing Values ---
(output removed)
--- Enter New Values ---
Authentication type: [local]: radius
Authentication method: [pap]:
Accounting type: [none]: 
Use RADIUS/TACACS Authorization: (y/n) [n]: y
Create users: (y/n) [n]: y
Cache passwords: (y/n) [n]: y
If server is down, should the system use local authentication: (y/n) [n]: y
(output removed)
```

## Create a role to apply the desired privileges

If necessary, use the **config role** command to edit or create a role with the privileges that you want to assign. Depending on your organization's needs, you may be able to use an existing role. For more about roles, refer to Managing roles and privileges.
 
## Create a group

If necessary, use the **config group** command to create a group.

Use the **system**, **port**, **modem**, and **powercontrol** subcommands as needed to apply the role containing the desired set of permissions.

Users will be added to the group each time a successful authentication occurs.

## Associate the ACL to users on the TACACS Server

The example below demonstrates how to create new users or add the ACL to existing users. Refer to your TACACS administratorâ€™s guide for more specific examples of configuration required for this functionality.

### Creating a TACACS User

To create TACACS users:

* On the TACACS server, create users.
* For each user, specify the ACL with the name of the group created on the Local Manager.

### Enabling Authorization on a TACACS User

To enable authorization on an existing TACACS user:

* Once the user is created and is able to authenticate to the Local Manager, add authorization by adding an ACL under the Exec service in your user or group.
* In most Unix TACACS deployments, you can edit the users file and add the following lines to either the group or the user:

```
service = exec {
acl = <acl name set for the group(s)>
}
```

### Enabling Authorization on a TACACS User with Cisco ACS

To enable authorization on an existing TACACS user with Cisco ACS:

* On your ACS, create a group for your users and then edit it by clicking Edit Settings.
* Then edit that group to include the following options: Shell (exec) and Access control list.
* Add a list of groups that you wish your users to be a part of, and then click Submit + Restart.

### Associate Uplogix Groups with users on the RADIUS Server

Create new users or add the ACL to existing users.

* The RADIUS Vendor specific attribute (VSA) "Uplogix-Version" is used to configure information specific to Uplogix.
* A new field called "Uplogix-User-Groups" in the VSA to hold a user's group information should be created.
	* The field can contain a single group name or comma-separated list of groups.
	* The group names must be established and configured on the Uplogix system separately from the RADIUS configuration.
	* On successful login on RADIUS, the VSA for Uplogix will be returned with the RADIUS response to the Uplogix device.

These steps are described in detail below.

* The Radius Dictionary contains these fields and is also available from the Uplogix support site.

```
Uplogix			10243
BEGIN VENDOR	Uplogix
ATTRIBUTE		Uplogix Version		1	string
ATTRIBUTE		Uplogix User Groups	3	string
ATTRIBUTE		Uplogix CLI Command	4	string
ATTRIBUTE		Uplogix Envoy Serial	5	string
ATTRIBUTE		Uplogix Task ID		6	string
END VENDOR		Uplogix
```