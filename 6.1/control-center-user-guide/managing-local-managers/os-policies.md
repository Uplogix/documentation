<!-- 5.5.3 -->

<div class='ucc' />Inventory > Local Manager or Inventory Group Page > Automation > OS Policies</div>

# Overview

The standard operating system policy feature allows network administrators to define an operating system standard for managed devices on a per make/model basis. Once the standard is defined at the inventory group or Local Manager level, the operating system file will be pushed to all applicable managed devices and stored locally as a specially named file called standard. If the current OS for a managed device deviates from its defined standard, the Control Center will alarm and potentially recover the device to the standard operating system.

# Defining the standard operating system

Begin by uploading the standard operating system file to the File Archive by choosing the file to upload and clicking the upload button.

![File Archive](http://uplogix.com/support/docs/img/6.0/file-archive-list.png)
 
Next, navigate to the Local Manager or Inventory Group page where the operating system standard will be defined. Select OS Policies under the Automation menu. Click add to create a new OS Policy.
 
![](http://uplogix.com/support/docs/img/6.0/create-os-policy.png)

Complete the policy information:
- **Make**: Make of the device where a standard operating system file will be applied.
- **Model**: Existing models are listed based on model types in the database, but new models can be entered when a user selects 'Other'.
- **Start**: The date at which the operating system policy will be implemented/activated.
- **Standard OS Category**: The category type of the previously uploaded standard operating system file in the Control Center File Archive.
- **Standard OS Name**: The name of the previously uploaded standard operating system file in the Control Center File Archive.
- ** Policy Actions**:
 - **Disabled**: Turn off recovery and alarming for a standard operating system policy after the policy has been implemented. The standard operating system file will still be stored as Standard on Local Managers affected by the policy.
 - **Alarm**: Alarm when the current operating system for a managed device does not match the operating system associated with the policy.
 - **Alarm & Recover**: Alarm and implement an automated recovery when a managed device does not meet the operating system policy. This action is available only for Cisco equipment running IOS or IOS-XE, where the operating system will only be recovered when the device is found without a configuration (such as when replacing a failed managed device with a new and unconfigured one).

Click **Save** to implement the operating system policy.

Once the operating system policy has been saved, the Control Center will begin staging the standard operating system file on the affected Local Managers.

# Standard operating system recovery

In most cases, the operating system policy will result in alarm when managed deviceâ€™s operating system does not match the standard. In the case of Cisco equipment running IOS or IOS-XE software, the Uplogix can be configured to automatically recover the managed device to the defined operating system standard.