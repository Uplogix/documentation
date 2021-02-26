<!-- 5.4 -->
<div class='ucc' />Inventory > Local Manager Summary > System > Virtual Slots</div>

There are a variety of cases where typical console device management may be impractical or impossible. For these deployments the Local Manager can be configured to use virtual device management ports. These virtual ports mimic the functionality of the physical serial interfaces on the Local Manager. Some cases where virtual ports are applicable include:

- Manage devices where the distance between the Local Manager and the managed device is too far for a RS 232 serial connection or where there is an inability to run additional cables.
- Manage devices already connected to a console server.
- Manage devices whose serial ports are being used for other purposes.
- Manage devices with IP connectivity but no serial connectivity.
- Manage devices using a virtual Local Manager running on a VMware ESXi server.

This feature requires the purchase of a virtual port license for each virtual port from Uplogix. All virtual ports are limited to virtual slot 4 on Uplogix hardware platforms. The maximum number of allowable virtual ports varies on a platform basis as follows:

- Uplogix 500 - 16 virtual ports supported
- Uplogix 5000 - 16 virtual ports supported

Virtual ports that terminate on the managed device (i.e., VTY/IP connection where no console server is involved) do not support all of the functionality supported for managed devices that are directly or indirectly connected to the Local Manager via a serial console port connection. The following driver functionality is not available in this case:

- LAN independence
- Bare metal restore
- ROMmon recovery 
- Password/Configuration recovery where boot loader configuration is required
- Power On Self Test (POST) data collection
- Automatic Rollback 
- xmodem and ymodem file transfers	

The following privileges are required to configure virtual ports:
- **config system slot** â€“ Configure a virtual slot and virtual ports.
- **show system slot** â€“ View virtual slot/port configuration.
- **config system clear slot** â€“ Clear virtual slot configuration.
- **config system clear port** â€“ Clear port/virtual port data from the database.

From the Local Manager page, create a virtual port by clicking Virtual Slots under the System configuration menu.

# Create a virtual port

![Uplogix Control Center](http://uplogix.com/support/docs/img/5.4/uplogi-control-center-add-virtual-slot.png)

Perform the following steps to configure a virtual port:

1.	**Slot**: Select the slot number for the virtual port (e.g., slot **4** for port 4/1). Slot 4 is the only available slot for virtual ports on Uplogix hardware platforms. Virtual Uplogix Local Managers can begin slot numbering with 1.
2.	**Port**: Enter the port number (e.g., **1** for port 4/1, where slot is 4).
3.	**IP**: This is the IP address of the managed device that the virtual port is terminating on or the IP address of the console server that has a serial connection to the managed device.
4.	**TCP Port**: Enter the TCP port for this virtual port connection (e.g., **22** for a SSH virtual port connection).
5.	**Protocol**: Select **ssh-vty** to have the Local Manager SSH directly to the managed device. Select **ssh** or **telnet** when the Local Manager connects to the end device through a console server.
6.	**Route over Management Ethernet**: Leave this box checked if the virtual port connection should always route out the primary/in-band management Ethernet connection, even when the Local Manager brings up an out-of-band connection.
7.	**Username**: Secure (SSH) virtual ports must authenticate to the end device in order to build the virtual port connectionâ€”this requires either a username/password combination or providing a username and then importing the Local Manager public key into the managed device for that user to use key authentication in lieu of password authentication for the user.
8.	**Password**: Enter the supplied usernameâ€™s password for the managed device when configuring a secure virtual port. This can be omitted if SSH key authentication is being configured on the managed device.
9.	**Host Key**: Optional if not running in FIPS mode. The Local Manager uses the host key to validate the identity of the managed device to which the virtual port is connecting. If left blank, the Local Manager will save the one it receives from the managed device when it connects for the first time.
10.	Click **Save** to add the virtual port.

# Modify a virtual port

To modify an existing virtual port definition on the Local Manager Virtual Slot configuration page, click on the **port number** (e.g., Port 4/1) hyperlink in the virtual port tableâ€”this will populate the virtual port form at the top of the configuration page with the current settings for the virtual port. Next, modify any of the virtual port settings in the form and then click **Save** to save the virtual port definition.

# Delete a virtual port

To delete an existing virtual port from the Local Manager Virtual Slot configuration page, click the **checkbox** to the left of the port to be deleted in the virtual port table and then click **Remove**.