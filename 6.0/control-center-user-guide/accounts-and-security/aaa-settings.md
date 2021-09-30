<!-- 5.4 -->
<div class='ucc' />Administration > AAA Settings</div>
<div class='ucc' />Inventory > Local Manager Summary > Security > Authentication</div>

# Overview 

The Control Center and Local Managers can perform user authentication, authorization, and accounting (AAA) functions locally or these functions can be deferred to one or more third-party AAA servers. 

Authentication/authorization/accounting settings for the Control Center can be managed globally from the AAA Settings page under the Administration tab. They can also be customized for specific portions of the deployment (i.e., Local Managers) from the appropriate group within the inventory.

# Control Center AAA

To configure AAA settings for the Control Center, and optionally for the entire inventory, click on *AAA Settings* under the Administration tab.
This page also includes strong password settings and other password-related settings such as lockout after login failure.

![Uplogix Control Center - AAA Settings](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-aaa.png)
 
To apply changes on this page to the Control Center only, click **Save**.

To copy the changes on this page to the root-level inventory group, click **Save and Copy**. Like other inventory settings, the authentication settings do not overwrite existing locally created settings unless you force them to do so. It will overwrite changes made in the top level of the hierarchy, but not those made in child groups.

To force the changes on this page on all Local Managers managed by this Control Center, select **Force settings to all appliances in hierarchy** before clicking **Save and Copy**.

# Inventory Group AAA

To configure AAA settings for an inventory group, open the detail page for that group and click *Authentication* from the Security menu to open the Authentication Settings page.

Settings available on the *Authentication Settings* page are inherited by all the members of this inventory group, except where they would overwrite existing, locally configured settings. Select **Force update on children** to overwrite all existing settings.

# Single Local Manager AAA

To configure AAA settings for a single Local Manager, navigate to the Local Manager and select Authentication from the Security menu.

# Accounting settings

Accounting events can be sent to a configured TACACS or RADIUS server using the start-stop (before and after each command) or the stop-only (after each command) model. This setting is not available if local authentication is used. Accounting applies to Local Managers only.
 
# Authentication settings

Most authentication settings available through the Control Center mirror those available through the **config system authentication** command on the Local Manager command line. They include the ability to select the type of authentication, to specify the necessary configuration information for each type, and to limit the number of concurrent sessions per account.
 
## Authentication Type and Method

Select the type of authentication to use. Local, RADIUS, and TACACS are available. If using TACACS or RADIUS, select the authentication method as well. PAP, CHAP, and MS-CHAP are available.

## Use RADIUS/TACACS Authorization

Some AAA servers support returning authorization keys that can be used by the Control Center to assign privileges to users. For information on configuring this, see [Using RADIUS/TACACS to manage privileges](#).

## Create Users

If users are managed on the authentication server, they are able to authenticate but may not have accounts on the Control Center or Local Managers. If this setting is enabled, the user is created if they do not exist. If RADIUS/TACACS authorization is not used, users initially have no privileges - so they are not able to log in, as this requires the login privilege.

## Cache Passwords

Enable this setting if the Control Center is configured to use authentication server(s) and Fail Over to Local is selected. This allows users to use a previously saved password if no authentication server is available and the Control Center fails over to local authentication.

## Fail Over to Local

Enable this setting to allow the Control Center to authenticate users locally when no configured authentication server is available. When using this setting, enable Cache Passwords to make the passwords available for local authentication. If Cache Passwords is not enabled, users will still be able to log in with locally defined passwords.

## Limit Maximum Concurrent Sessions and Maximum Number of Concurrent Sessions

These settings allow you to limit the number of open sessions that any user may have on any particular Local Manager at a given time. Set the maximum number to 0 to allow unlimited concurrent sessions.

# Authentication and Accounting Servers

If the Control Center or Local Managers are configured within the inventory to use RADIUS or TACACS, at least one of the appropriate type of server must be configured. Up to four authentication servers and up to four accounting servers can be specified for redundancy. All must be of the same type, either RADIUS or TACACS. If an authentication server fails to respond, the next server is queried; the first response determines whether the authentication is successful.

For each server, enter the IP address and port; then enter and confirm the secret. For RADIUS servers, the default port is 1645 or 1812; for TACACS, the default port is 49.

To remove server information already configured, click the *Clear* button associated with that server.

![AAA Servers](http://uplogix.com/support/docs/img/6.0/aaa-servers.png)
 
# Choosing how to Apply AAA Changes 

When making changes on the *Administration > AAA* page, apply them in three ways:

* Update AAA settings only on the Control Center -- click *Save*.
* Update AAA settings on the Control Center and at the root level of the inventory without changing settings on Local Managers currently in the inventory -- click *Save and Copy*.
* Update AAA settings globally, overwriting existing settings on the Control Center and all Local Managers -- select *Force settings to all appliances in hierarchy*, then click *Save and Copy*.
 
![AAA Settings](http://uplogix.com/support/docs/img/6.0/aaa-settings.png)

When making changes at the inventory group level from the Authentication page, apply them without changing settings on Local Managers currently in the group or overwrite the Local Managers' authentication settings.

* Update AAA settings for the group without changing settings on Local Managers currently in the inventory&mdash;click *Save*.
* Update AAA settings for the group, overwriting existing settings on all Local Managers in the group and its child groups&mdash;select *Force updates on children*, then click *Save*.
 
![AAA Force Update](http://uplogix.com/support/docs/img/6.0/aaa-force-update.png)

# Strong Passwords

Configure strong passwords at any level within the inventory, on the Control Center only, or globally. The password requirements can be tailored separately for different groups or Local Managers within the deployment. 

For password restrictions to take effect, *Use strong passwords* must be selected. To remove strong password restrictions temporarily, clear **Use strong passwords** while leaving the restrictions configured.

Restrictions include:

|Setting	|Description|
|:---|:---|
|Require mixed case	|Password must have both capital and lowercase characters<br><br>Valid password example: PassWord|
|Require numbers and punctuation|	Password must include at least one numeral and at least one symbol.<br><br>Valid password example: P@ssW0rd|
|Reject variation of Login ID	|Password cannot be derived from the login ID<br><br>Invalid Example:  admin1|
|Reject variation of previous passwords	|Obvious variations on the previous password will be rejected. The following examples assume that the previous password was P@ssW0rd<br><br> - change of case only; p@SSw0rD will be rejected<br><br> - reversed character sequence; dr0Wss@P will be rejected<br><br> - doubled sequence; P@ssW0rdP@ssW0rd will be rejected<br><br> - string containing the earlier password; myP@ssW0rd! will be rejected|
|Reject word in dictionary<br><br>Reject standard substitutions (@ for a, 3 for e, etc.)|	If both options are selected, users may not set passwords such as p@$$w0rd.<br><br>Valid password example: P&ssW*r#|
|Reject sequences in numbers or letters	|Users may not set passwords that consist of all the letters or numbers on one row of the keyboard, in sequence either from left to right or right to left, or a character string that contains such a sequence. Partial or broken sequences such as abc!defg or qwerty12 may be used.|
|Reject previous password<br><br>Number of previous passwords to check|	Recently used passwords may not be reused|
|Reject single character difference from previous password	|When changing a password, at least two characters must be changed|
|Enforce minimum password length<br><br>Minimum password length	|Keeps users from setting passwords short enough to be easily guessed.|
|Expire password<br><br>Number of valid days	|Forces users to change their passwords periodically.|
|Number of invalid attempts before lockout<br><br>Lockout duration in minutes	|Specify the maximum number of times a user can attempt to log into a Local Manager before the Local Manager refuses further attempts, and the length of the lockout period. Set the number of attempts to 0 to disable lockout protection. The default lockout time is 30 minutes. These settings apply only to Local Managers, not to the Uplogix Control Center.|

> Do not create a password that ends with a space character. When an attempt is made to log into a Local Manager using a password that ends with a space, the Local Manager strips the space character and the login fails.