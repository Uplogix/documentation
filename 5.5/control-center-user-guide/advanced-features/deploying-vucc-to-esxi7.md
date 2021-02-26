# Overview
This article describes the deploying of an Uplogix Virtual Control Center to an ESXI environment running 7.0 or later. Before following these instructions, please be sure you have read the requirements detailed in Deploying a Virtual Control Center.

> These instructions are very similar for deploying to ESXi 6.5 and 6.7 using the web interface.  There are known issues with uploading the Control Center VM using a browser to ESXi 6.5.  You can work around the issues by using the command line OVF Tool available from VMware.

Log into your VM host using a supported browser. Then select Virtual Machines from the left menu.  In the Virtual Machines view, select Create / Register VM.  This will pop up a wizard to walk you through the steps to deploy the Control Center.
 

Step 1: Select creation type.
Select Deploy a virtual machine from an OVF or OVA file.
 

Step 2: Select OVF and VMDK Files
Click in the blue section to browse to the OVA file you downloaded from Uplogix.  Once you have selected the OVA file, enter a name for the virtual machine.  This name is can be whatever you like it to be.  It is only used by the customer.
 

Step 3: Select storage
Select a datastore for the virtual machine to deploy to.
 

Step 4: Deployment options
You may configure these settings as desired by the customer.  Using Thin disk provisioning is recommended.
 

Step 5: Ready to complete
Review you settings and if they look good, select Finish.
 

At this point, the wizard popup will close and you will return to the Virtual Machine view.  At the bottom of the screen, you should see six disks uploading.
 

Once the disks have uploaded, you will see the new virtual machine listed.  If you used thin provisioning, the Used space will show about 443 GB.  The upload of all six disks can take about 20 minutes.  This time can be extended due to network or disk performance in your environment.
 

You can now click on the deployed virtual machine for further details.  See below for an example.
 
 

Configure the Control Center to Auto Start

Select Manage from the left menu, then Autostart under Advanced settings.
 

You may need to enable Autostart for the server by selecting Edit settings.
 

Once the server is using Autostart, select the Control Center virtual machine and then click Enable.
 

Autostart for the virtual machine should change from Unset to a number.  This number is the order in which virtual machines will be started.  In this example, since there is only one virtual machine, the number is 1.
 
