# Overview
This article describes the deploying of an Uplogix Virtual Control Center to an ESXI environment running 6.7 or earlier. Before following these instructions, please be sure you have read the requirements detailed in [Deploying a Virtual Control Center](https://uplogix.com/docs/control-center-user-guide/installation-and-configuration/vucc-deployment).
# Deploying via Web Browser

There is a known issue deploying and exporting "large" VMs with the ESXi web client in early versions of 6.5 and 6.7.  If you try to deploy the Control Center VM using a browser and it fails about half way through, we recommend using the command line VMware OVF Tool. This tool is actively maintained and supports ESXi 6.5 and 6.7.  You can download it from VMware (https://www.vmware.com/support/developer/ovf/).  This deployment issue appears to be fixed in ESXi 6.7.0 Update 1.  Please contact Uplogix Support if you have any question about using the OVF Tool.

# Deployment

Connect to your VM host and select **File > Deploy OVF Template...**.  Although this menu item says OVF, it will let you select OVA files as well.  An OVA file is just a package of the OVF file and VMDK files in the TAR format.

![vSphere Client Deploy OVF Template](http://uplogix.com/support/docs/img/5.4/vucc/image001.png)

## Select OVA

Select the vUCC OVA file you previously downloaded.

![Select OVA](http://uplogix.com/support/docs/img/5.4/vucc/image002.png) 

## Ignore Warning

Depending on the version of your VMware host, you may see a similar warning window below.  This is normal and will not impact the deployment of the vUCC.  Click Yes to proceed.

![Ignore Warning](http://uplogix.com/support/docs/img/5.4/vucc/image003.png)

## Select Datastore

Select a datastore with enough free space to handle your deployment (see [Requirements](#requirements)).

![Select Datastore](http://uplogix.com/support/docs/img/5.4/vucc/image004.png)

## Select Disk Format

Select **Thin Provision** or **Thick Provision** as appropriate to your deployment size for the disk format.  If you have determined that you should use thick provisioning, you may choose lazy or eager zeroed based on your own preferences.

![Select Disk Format](http://uplogix.com/support/docs/img/5.4/vucc/image005.png)

## Map Network

Map the source network to the destination network according to your needs.  The default is frequently acceptable.

![Map Network](http://uplogix.com/support/docs/img/5.4/vucc/image006.png)

## Finish

Ensure **Power on after deployment** is **not** selected.  Click Finish to begin the deployment of the vUCC.

![Finish](http://uplogix.com/support/docs/img/5.4/vucc/image007.png)

# Deployment Time

The progress bar is not very accurate with its time estimation.  Since the vUCC has 6 VMDKs (disks) inside the OVA, you will frequently see an estimate like *5 minutes remaining*, but then it will move on to the next disk and say the same estimate for remaining time.  Typical deployment times vary from 25 minutes (SSD RAID 10) to 3 hours (SAS RAID 5).  The deployment time is heavily dependent on the speed of the VMware host datastore and may increase when a datastore is heavily shared by other VMs.  Network speed is also a factor and we recommend you use a gigabit link.

![Deployment Time](http://uplogix.com/support/docs/img/5.4/vucc/image008.png) 

Once the deployment has completed successfully, click **Close**.

![Deployment Time](http://uplogix.com/support/docs/img/5.4/vucc/image009.png)

# Default Settings

The following shows the default settings for the vUCC.

![Default Settings](http://uplogix.com/support/docs/img/5.4/vucc/image010.png)

The following shows the default settings for the evaluation vUCC.

![Default Settings](http://uplogix.com/support/docs/img/5.4/vucc/image011.png)

# Edit Settings

If you need to edit any of the deployment settings, right-click on the VM's name.  Select **Edit Settings...** to change the number of CPU cores, memory, or network settings.

![Edit Settings](http://uplogix.com/support/docs/img/5.4/vucc/image012.png)

# Power On

Once the settings have been configured, power on the VM.  You can do this by right-clicking the VM name again or using the green "play" icon.

![Power On](http://uplogix.com/support/docs/img/5.4/vucc/image013.png)

# Automatic Startup

We recommend that you configure the vUCC for automatic startup and shutdown.  Versions 5.4+ of the vUCC contains open source vm tools which allow VMware to do a soft shutdown of the VM.  While problems usually do not occur with a hard power off, we recommend that you avoid it when possible.  Hard power off can occasionally cause file system corruption.

![Automatic Startup](http://uplogix.com/support/docs/img/5.4/vucc/image014.png)

# Adjusting Memory

If running the VM with anything other than 8 GB of RAM, the memory settings for the vUCC application will need to be changed:

* Enter **vi /etc/sysconfig/embassy.overrides**
* Move the cursor over the number 8 on the line which reads **RAM=8**
* Press **r**, then enter the number of gigs of RAM allocated to your VM
* Type **:wq **to save the file and exit from the editor
* Restart the vUCC application by entering the commands **ucc stop** and **ucc start**.

# IP Configuration

After powering the VM on, click the **Console** tab.  Once the vUCC has finished booting, log in as user *emsadmin* with password *password*.  You may miss the login prompt as information about the database writes to the console.  If you see *Database "UPLOGIX" warm started*, hit enter once and you will be presented with the login prompt.

To configure static IP addresses for the vUCC and to complete the provisioning process, please continue to [Provisioning](https://uplogix.com/docs/control-center-user-guide/installation-and-configuration/provisioning).

![Test](http://uplogix.com/support/docs/img/5.4/vucc/image015.png)