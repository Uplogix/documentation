# Overview

As of LMS version 6.2, the Uplogix Control Center can now be deployed to a Microsoft Azure environment. This document details the installation and provides configuration recommendations. Please contact Uplogix Support if you have any questions or would like assistance during deployment.

# Scaling Support

The current default VHD disk configuration supports 50 Local Managers. By editing a configuration file to increase expected memory allocation, the same VHDs can be used to support up to 500 Local Managers. With further customization to increase the size of disk2, support for up to 2000 Local Managers is possible. Recommended Azure deployment steps, configuration, sizing, and costs will be described in this document.

# Download

Download the Azure ZIP file and sha256 file from the Support Site at uplogix.com/support/account.

Files will be tagged with **-Azure.zip**. For example:

* vUCC-520GB-v620-GA-38768-Azure.zip 
* vUCC-520GB-v620-GA-38768-Azure.zip.sha256

Optionally, verify the checksum of the ZIP file.  This will ensure that you have downloaded the file properly without any data loss or corruption.

Linux example:

```
sha256sum -c vUCC-520GB-vxxx-GA-xxxxxx-Azure.zip.sha256
vUCC-520GB-vxxx-GA-xxxxxx-Azure.zip: OK
```

Windows example:

```
certutil -hashfile .\somefile.ova SHA256
```

In Windows, you'll need to manually compare the hash with the contents of vUCC-520GB-vxxx-GA-xxxxxx-Azure.zip.sha256.

# Decompress

Unzip the file.  This is supported by Windows 10 in the File Explorer or a command line.  While the zip is only about 4GB in size, it will decompress to 520GB.  It is composed of two drives.  One is 40GB and is the boot drive (vUCC-520GB-vxxx-GA-xxxxxx-Azure-disk1.vhd).  The other is 480GB (vUCC-520GB-vxxx-GA-xxxxxx-Azure-disk2.vhd).

> Note: decompression may take 30-60 minutes depending on your system capabilities.

# Prepare Azure

To upload a VHD and create a VM, you will need to have a *Subscription*,* Resource Group*, and *Storage Account* set up in Azure.  If you have questions about how to do this, please contact Uplogix Support.  The *Storage Account* will also need a *Container*.

If you are unsure of what settings to use for the *Storage Account*, we recommend a *Region* that is closest to your primary users.  Standard performance and locally redundant storage (LRS) should be fine.

![](/support/docs/img/6.2/azure/createStorageAccount.png)

![](/support/docs/img/6.2/azure/createStorageAccount2.png)

![](/support/docs/img/6.2/azure/createStorageAccount3.png)

![](/support/docs/img/6.2/azure/createContainer.png)
 
# Upload VHDs

You can use the web page at portal.azure.com to upload the files into the *Container*, but we recommend using the Microsoft Azure Storage Explorer or PowerShell.  The web page usually works for uploading disk1 (40GB) but is both slow and frequently can time out when uploading disk2 (480GB).  The Storage Explorer application transfers data faster and handles timeouts well.

https://azure.microsoft.com/en-us/features/storage-explorer/

The VHD files should be uploaded as Blob type “Page Blob”.

![](/support/docs/img/6.2/azure/uploadVHDs.png)

![](/support/docs/img/6.2/azure/uploadVHDs2.png)

![](/support/docs/img/6.2/azure/uploadVHDs3.png)

You can also verify that the VHDs have been uploaded from the web.

![](/support/docs/img/6.2/azure/uploadVHDs4.png)
 
> Note: on a 1Gbps internet connection, it will take about one hour to upload both VHD files.

# Create Image

Create an image from disk1.  We recommend using the same Region that was selected for the Resource Group and the desired VM.

* OS type must be Linux
* VM generation can be Gen 1
* Storage blob should be disk1
* Account type can be Standard HDD
* Click to Add data disk
* Select disk2 for the Data disk
* Finally click Review+Create

If validation succeeds, click Create.

![](/support/docs/img/6.2/azure/createImage.png)

![](/support/docs/img/6.2/azure/createImage2.png)

![](/support/docs/img/6.2/azure/createImage3.png)

# Create VM from Image

Navigate to your new image and click *Create VM*.  For *Size*, the default configuration requires 2 CPUs and 4GB of memory.  We recommend selecting “Standard_B2s”. You can leave the *Administrator* account settings defaulted to SSH public key.  The key pairs are not required for deployment.  For inbound ports, allow HTTP (80), HTTPS (443), and SSH (22).  *License* type can be *Other*.  Click on “Next : Disks”.

![](/support/docs/img/6.2/azure/createVM.png)

![](/support/docs/img/6.2/azure/createVM2.png)
 
For OS disk type select Standard HDD (LRS).

![](/support/docs/img/6.2/azure/createVM3.png)

Networking settings can all remain as their defaults.

![](/support/docs/img/6.2/azure/createVM4.png)

Continue with *Next : Management*.  We suggest setting *Boot diagnostics* to *Enable* with custom storage account.  Then select your storage account from earlier.  This will allow you to use the Serial console if any debugging is needed.

![](/support/docs/img/6.2/azure/createVM5.png)

*Advanced* settings and *Tags* are not required.  Click on *Review + create*.

![](/support/docs/img/6.2/azure/createVM6.png)

If validation succeeds, continue with *Create*.  This step usually takes a couple minutes.

![](/support/docs/img/6.2/azure/createVM7.png)

![](/support/docs/img/6.2/azure/createVM8.png)
# Allow Additional Ports

The UCC uses the following ports: 22, 80 (optional), 443, 8443, 2222, 2244.  If you navigate to *Networking*, the default page should list your primary network interface and inbound port rules. Click *Add inbound port rule* to allow inbound traffic to each port.

![](/support/docs/img/6.2/azure/addInboundPort.png)

![](/support/docs/img/6.2/azure/addInboundPort2.png)
 
# Configure the UCC

The database and web application do not start by default to avoid possible corruption that could occur while troubleshooting any deployment issues.  Log in over either the serial console or SSH as *emsadmin* and *password*.  Then run **sudo su -** to become root. Run **ucc chkconfigon** and **reboot**.  On the next restart, all services will start automatically.

![](/support/docs/img/6.2/azure/configureUccOn.png)

We recommend that you change the password for the *emsadmin* user.

```
[emsadmin@UplogixControlCenter ~]$ passwd
Changing password for user emsadmin.
Current password:
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```



# Setting Up Pulse
The Pulse feature requires a secondary network interface on the Control Center. You will need to create a second network interface, attach it to your VM, and allow inbound traffic to port 7 (echo) for the interface.

Start by creating a new *Network interface*.  You can use the same *Subscription*, *Resource group*, *Region*, *Virtual network*, and *Network security group* that your VM is already using.

![](/support/docs/img/6.2/azure/createNetworkInterface.png)

![](/support/docs/img/6.2/azure/createNetworkInterface2.png)

![](/support/docs/img/6.2/azure/createNetworkInterface3.png)

Assign a public IP to the new network interface.  Navigate to *IP configurations* and select the Primary config.

![](/support/docs/img/6.2/azure/createNetworkInterface4.png)

*Associate a Public IP address* to this config.  Then create a new public IP address and select Save.

![](/support/docs/img/6.2/azure/createNetworkInterface5.png)

Before associating the new network interface with your VM, you must stop it.  VM *Status* should show *Stopped*.  Navigate to *Networking* and click *Attach network interface*.

![](/support/docs/img/6.2/azure/attachNetworkInterface.png)

Add an inbound port rule for port 7.

![](/support/docs/img/6.2/azure/attachNetworkInterface2.png)

*Start* your VM and log in.  Run **ip addr list** and you should see a second interface.

![](/support/docs/img/6.2/azure/attachNetworkInterface3.png)

<div class="warning">UPDATE IN PROGRESS: This section is still being updated. Please contact Uplogix Support for assistance.</div>

# Cleanup

Unless you plan to deploy another instance of the UCC for High Availability (HA), you can now delete the *Image* that was used to create the VM.  You can also delete the uploaded VHD files that are *Page blobs* in your storage account container.  You can also delete the *Container* if you created this just for uploading the UCC.

Do not delete the storage account if you still want the serial console enabled for future use.  There is a generated container that makes the serial console work usually called *bootdiagnostics-[vmname]-[id]*.

![](/support/docs/img/6.2/azure/cleanupContainer.png)

# Cost Forecast

If you used the settings described above (size: Standard_B2s, Standard HDD (LRS)), with 50 of fewer Local Managers you should expect a cost of about $950 a year, or $2.60 a day.

We will continue to update cost forecasts as more data becomes available.

# Ready to Provision

You can now proceed to [Control Center Provisioning](https://uplogix.com/docs/6.2/control-center-user-guide/installation-and-configuration/provisioning)