<!-- 5.4 -->

# Overview

The Control Center provides users with the ability to open SSH connections to Local Managers that pass through to the console port of a managed device via the SSH Applet. Under normal circumstances, the SSH Applet establishes an SSH connection to the Local Manager. In the unusual event that the applet is unable to establish an SSH connection to the Local Manager, the SSH Applet Failover feature allows configuration of the SSH Applet so that it fails over to establishing an SSH connection directly to the managed device.

> Many of the valuable Uplogix features such as session logs, events, and configuration rollback become unavailable when the SSH Applet fails over to connecting directly to the managed device, as the Local Manager is out of the connection loop in this scenario.

# Device Properties

This feature is activated by adding one or both of the following device properties to the Local Manager port for the managed device.

### _applet_failover_ssh_fingerprint

Defines the SSH fingerprint for the managed device.

The SSH Applet will only establish a failover SSH connection to the managed device if the fingerprint it receives from the managed device matches the fingerprint value stored in this device property. 

This property can be configured through the Local Manager CLI and via the Control Center.

### _applet_failover_ssh_ip

Defines the IP address that the SSH Applet should attempt to establish an SSH session to in the case where the applet fails to connect to the Local Manager. 

This property is only required if a management IP address is not defined for the managed device within the Local Manager or Control Center.  

If a management IP address exists for the managed device and this property is not defined, then the SSH Applet will attempt the failover SSH connection to the defined management IP address.  

If this property IS specified/defined, then the SSH Applet failover feature will use the IP address contained in this property rather than the management IP address. 

This property can be configured through the Local Manager CLI and via the Control Center.

# Example

The following example walks through the process of configuring SSH Applet Failover to a Cisco 3925 router connected to port 1/2 of the Local Manager.

## Determine the SSH Fingerprint for the Managed Device

Part of enabling SSH Applet failover to the managed device involves configuring the Local Manager with the SSH fingerprint of the managed device. Initiate an SSH session to the managed device via a terminal session or application such as PuTTY. The managed device fingerprint will display with a question asking whether to continue connecting. This assumes the PC/workstation does not have the managed deviceâ€™s RSA key in its known host file.  If the fingerprint is not presented with a question asking whether to continue, then edit the SSH known host file on your PC/workstation to remove the entry for the managed device.  Here is an example using a Linux, Unix or Mac terminal session:

```
/Users/admin > ssh admin@192.0.2.100
The authenticity of host '192.0.2.100 (192.0.2.100)' can't be established.
RSA key fingerprint is b7:b7:9b:ce:bc:44:82:36:ca:92:71:65:fe:fd:4f:43.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.0.2.100' (RSA) to the list of known hosts.
```

An example of the fingerprint in a Putty popup window is shown below:

![](http://uplogix.com/support/docs/img/cc-user-guide/image165.png) 

**Copy the SSH fingerprint.** It is a required device property that will be set up in the next step.

## Configure Device Properties via the Local Manager CLI

Log into the Local Manager and navigate to the port that is to be configured for SSH Applet failover and enter the device property editor by issuing the following commands:

```
[admin@UplogixLM]# port 1/2
LRT-3925 cisco CISCO3925-CHASSIS IOS 15.1(4)M
         3925
[admin@UplogixLM (port1/2)]# config properties
[config properties]#
``` 

Now configure the **_applet_failover_ssh_fingerprint** device property for the managed device SSH fingerprint (determined in the previous step) with the following command (where there is a space between the property and the fingerprint value):

```
[config properties]# _applet_failover_ssh_fingerprint b7:b7:9b:ce:bc:44:82:36:ca:92:71:65:fe:fd:4f:43
[config properties]# show
_applet_failover_ssh_fingerprint: b7:b7:9b:ce:bc:44:82:36:ca:92:71:65:fe:fd:4f:43
```

If there is no management IP address for the managed device configured in the Local Manager, or if the failover IP address that should be used is different from the configured management IP address, then the **_applet_failover_ssh_ip** device property should be configured to specify the failover IP address for the managed device. The **show info** command can be used to determine the management IP address for a given device. The following example shows the managed device to have a management IP address of 192.0.2.100:

```
[admin@UplogixLM (port1/2)]# show info
Hostname: LRT-3925
Description: 3925
Make: cisco
Model: CISCO3925-CHASSIS
OS: IOS
OS Version: 15.1(4)M
Management IP: 192.0.2.100
Current CPU Utilization: 0%
CPU Utilization (1 minute average): 1%
CPU Utilization (5 minute average): 1%
Total Memory: 762273884 bytes
Used Memory: 52811412 bytes
Free Memory: 709462472 bytes
```

To demonstrate how to set this device property, suppose that the SSH Applet should fail over to IP address 192.0.2.200 if a SSH session cannot be established to the Local Manager. Issue the following commands to enter the device property configuration editor on the managed device port and set the applet failover IP address:

```
[admin@UplogixLM (port1/2)]# config properties
[config properties]# _applet_failover_ssh_ip 192.0.2.200
[config properties]# show
_applet_failover_ssh_ip: 192.0.2.200
_applet_failover_ssh_fingerprint: b7:b7:9b:ce:bc:44:82:36:ca:92:71:65:fe:fd:4f:43
[config properties]# exit
```

Alternatively, device properties can be set via the Control Center. Log into the Control Center, navigate to the Local Manager in the Inventory, click on the port for the managed device in the Device section of the Local Manager summary page, and click the Properties link in the left navigation bar. The following page appears so device properties can be added or deleted:

![](http://uplogix.com/support/docs/img/cc-user-guide/image166.png)
 
# Usage

Once device properties are configured for a managed device as specified above, the SSH Applet failover feature is configured and active. To use the SSH Applet to access the console port of a managed device, connect to the web interface of the Control Center and navigate to the Inventory page. Select a Local Manager from the Inventory tree to bring up its detail page. Launch the Control Center applet by clicking on the SSH button. Should the SSH Applet fail to establish an SSH session to the Local Manager, the applet will then attempt to establish an SSH session directly to the managed device.