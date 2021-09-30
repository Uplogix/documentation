All Uplogix Control Center (UCC) upgrades must be performed by a support representative. If you are interested in upgrading your deployment, here is a quick checklist of things to do.

# Schedule an upgrade time with Uplogix Support

Uplogix Support is available 24/7 via email or phone.

* 888-663-6869
* 512-857-7070 
* support@uplogix.com

We typically perform only one upgrade a day as some upgrades may require more time than others depending on the features added to the software. Keeping upgrades to one a day allows us as much time as needed to complete the UCC upgrade and to begin upgrading the deployed Local Managers.

If you require more information on the new features included in a patch or a more detailed estimate of how long a specific upgrade will take, include these in your message to Uplogix Support.

Prior to the scheduled upgrade time, we will send a link to a Webex or Microsoft Teams meeting. This will allow us to see and control your computer so we can perform the upgrade remotely on your local network.

> Your security policy may prohibit us from controlling or even seeing your desktop. In those cases, we will make our best effort to find a solution that satisfies your security policy.

# Ensure Control Center availability 

Please ensure the UCC has IP connectivity and is reachable from your workstation. It is likely we will need to reboot the sever during the install process, so please plan the downtime accordingly.

**Average downtime of the UCC during an upgrade is 30-60 minutes.**

# Verify emsadmin access

As part of the upgrade process, we will log into the UCC's Linux layer as *emsadmin*. The default password for this account is *password*, but it may have been changed since installation.

> Uplogix Support does not store customer password information. If you have lost emsadmin's password, there is a way to recover access, but it will require physical access to the UCC.

# Prepare the Control Center for file transfers

Once we are able to access the emsadmin account, we will need to ensure that we area able to transfer files to the UCC. Typically we will download the required version from our Support Site to your computer, and then transfer it (via FTP or SCP) to the UCC. If you are running a Windows computer, we may need some additional tools to do an FTP or SCP transfer, such as pscp, WinSCP or Cyberduck FTP Server.

If your UCC has access to the internet, we may be able to directly download the files from the Uplogix servers using wget or SCP.

Our software downloads are located here: [uplogix.com/support/account](https://uplogix.com/support/account/)

The upgrade files are located in the folder of the latest LMS version.

For the UCC upgrade, we will need the **embassy.tar.gz** and any files that start with  **osUpdates**. 

A **.bin** file is required to upgrade your Local Managers. The version denoted with a **g** are certified to be FIPS compliant for customers that require it.

The **.bin** file denoted with **-all** is a universal update file for both the 500/5000 and LM80/LM83X Local Managers. If you are in a low bandwidth situation, you can use the smaller hardware-specific update files denoted with a **5** or **8** depending on your platform.

> Please see the complete [release notes for v6.2](https://uplogix.com/docs/6.2/knowledge-base/software/release-notes-6.2), as there are important changes relating to the Operating System of the UCC. Customers on older versions of the UCC (v6.0 or older) will need to have the UCC upgraded in steps to get to v6.2, and will require additional upgrade files. Please contact Uplogix Support for information on what files are needed prior to the upgrade. 

If you have questions regarding our upgrade process, please feel free to [contact us](mailto:support@uplogix.com).