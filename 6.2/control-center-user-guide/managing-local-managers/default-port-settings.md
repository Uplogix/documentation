<!-- 5.4 -->
<div class='ucc' />Inventory > Group</div>

Use the **config settings** command on the Local Manager to define how the Local Manager communicates with the device connected to a given port. On the Control Center, these settings can be defined and applied to more than one port; they could apply to all devices of a specific make, model, or operating system. For example, define a default port settings profile for all Cisco devices to set the terminal speed to 19200 for any Cisco device.

Default port settings are inherited from inventory groups, so a setting profile defined at the root group is inherited by the entire deployment. Settings profiles defined in a child inventory group are only inherited by its child groups and the Local Managers in those inventory groups. Therefore, it is possible to have default port settings for a Cisco 3925 that set the terminal speed to 9600 in Group 1, and identically named default port settings in Group 2 that set the speed to 19200. This type of situation can also occur when a child group already has default port settings stored under the same name as the settings you create in the parent group.

> **NOTE:** The settings presented on this page mirror those found in the **config settings** command on the Local Manager CLI. See [Configuring Port Settings for Managed Devices](http://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/configuring-port-settings) for more information.

To access the *Create Default Port Settings* page, click *Default Port Settings* under the *System* configuration menu of an Inventory Group page. 

![Uplogix Control Center Port Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-inventory-port-settings.png)

Any default settings that have been created are listed. Use the View Settings page to edit, remove, or add default port setting profiles.

Select an existing profile or click *Add* to create a new one.

![Uplogix Control Center Port Settings Cisco](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-inventory-port-settings-cisco.png)

Removing a port setting profile does not affect the devices where the settings have already been applied. For example, referring to the screen above, if the Cisco settings are removed, the configuration of Cisco devices is not changed. If you then connect a Cisco device to a Local Manager, the Cisco profile is no longer present and the port settings will manually need to be configured using the **config settings** command.

The Create Settings option is not available if the inventory group is empty. However, the Default profile can be edited. This default port settings profile can be changed but not deleted.

Specify as much or as little information as necessary when creating settings. The Local Managers that inherit these settings will apply them to any port that matches all the information given. For example, specifying **cisco** will match all Cisco devices. Specifying cisco and 3925 will match only Cisco 3925 devices. If the desired device make is not listed, choose **native**.

Select the settings to change using the checkboxes on the left, and modify the values as needed.

When editing existing default port settings, specify whether to force the update on any child groups within the affected inventory group. Otherwise, the settings are only updated in the current inventory group. 