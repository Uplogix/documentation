# Overview

For the best and most secure experience, Uplogix Local Managers should always run the latest version of LMS. Uplogix generally releases two new versions of software each year, but may also release patches if important bugfixes or security updates are required.

To ensure proper operation of the Local Manager with the Control Center, both need to be running the same minor revision of software. That is, **the first two numbers of the version** need to be the same.

For example, a 6.2.0 Local Manager will work fine with a 6.2.1 Control Center. A 6.1 Local Manager, however, will not synchronize with a 6.2.x Control Center.

<div class='danger'>LMS 6.2 only supports upgrades from Local Managers running 6.1.x. Customers on previous versions will need to upgrade multiple times. Contact Uplogix Support for more information.</div>

# About the Upgrade

Here's what happens when you upgrade a Local Manager:

1. The bin file is downloaded to the Local Manager
2. The bin file is decrypted and verified
3. Upgrade files are unpacked onto the filesystem
4. The Local Manager restarts to perform the upgrade.

The Local Manager will be available until Step 4. During the upgrade, the operating system will be up and responding to pings, but SSH will be unavailable until the upgrade is complete.

# Choosing the Right Software

![Software Downloads for 6.2](/support/docs/img/6.2/software_downloads_6.2.png)

Uplogix provides multiple software bin files to best match your deployment. 

## For Most Customers

Most customers will want to download the bin file tagged with **-all.bin**. This file contains software for both the 500/5000, LM80/LM83X, and Virtual platforms. 

## For FIPS Customers

FIPS-compliant versions of LMS are tagged with the **g** letter. Most customers will want to download the bin file tagged with **-allg.bin**. This file contains FIPS-compliant software for both the 500/5000 and LM80/LM83X platforms.

## For Low Bandwidth or Single Platform Customers

For environments where bandwidth is a concern, Uplogix provides smaller platform-specific bin files for updating Local Managers.

* Bin files tagged with **-5** are for 500/5000 and **Virtual Local Managers**
* Bin files tagged with **-8** are for LM80/LM83X Local Managers

Use the **g** version as needed for FIPS environments.

> Previous EOL platforms are no longer supported and cannot be upgraded.

# Download Software

Visit your Uplogix Support Site account page at uplogix.com/support/account.

<div class='warning' />An active maintenance contract is required to access the Uplogix Support Site account page and/or download software. If your maintenance contract has expired, please contact Uplogix Support.</div>

Find the green button marked *Download Software*.

![Support Site Software Downloads](http://uplogix.com/support/docs/img/6.2/software_downloads_list.png)

Click the folder link for your desired software version.

![Software Downloads for 6.2](/support/docs/img/6.2/software_downloads_6.2.png)

Click the link to download the bin file to your desktop.

> Customers with Local Managers on older versions (**6.1.0** or older) will need to upgrade in steps to get to 6.2. Please contact Uplogix Support for information on your upgrade path and what files are needed prior to the upgrade.

# Upgrading via SCP, FTP, and HTTP

SCP, FTP, and HTTP require the lms.bin file to be staged on an appropriate server. Push the file to an SCP, FTP, or HTTP server.

> The Control Center can be used as an SCP target because of its Linux operation system. Use a program like WinSCP or pscp to transfer the bin file to /home/emsadmin.

<div class='danger' />While possible, please do not use the Uplogix Support Site as an HTTP target if you upgrade a large number of Local Managers.</div>

Log into your Local Manager and use the **config update** command to initiate the upgrade. You will need to specify the IP address or hostname of the target and the path to the file.

For example:

```
config update scp user@198.51.100.172:UplogixOS-6.2.0.38768-all.bin
```

or


```
config update ftp user@198.51.100.172:UplogixOS-6.2.0.38768-all.bin
```

or

```
config update http http://198.51.100.172/UplogixOS-6.2.0.38768-all.bin
```

# Upgrading via the Control Center

To upgrade Local Managers from the Control Center, please refer to *Control Center User Guide*, [Upgrading Local Managers](http://uplogix.com/docs/control-center-user-guide/managing-deployment/upgrading-local-managers).

# Upgrading from a USB flash drive

Flash drives are a useful alternative if the Local Manager isn't on the network or is in a remote location.

## Prepare USB Drive

The flash drive should be formatted with the FAT16 filesystem. If the drive is formatted with FAT32, it must be removed from the Local Manager after it reboots to complete the upgrade.

## Add "upgrade.mnf" File

Download the **upgrade.mnf** file from the Uplogix Software Directory of the version you wish to upgrade to and copy it to the root directory of the USB drive.

## Plug in USB Drive

Use a free USB slot on the front of the Local Manager. Allow a few seconds for the system to recognize the new drive.

## USB Upgrade via Front Panel

Press the center button on the keypad to enter the Local Manager menu.

Scroll down and select *Update*.

Verify that *Update to [version]?* message matches intended version.

Scroll left and select *Yes*.

The upgrade will now continue on its own. While the software is transferred to the Local Manager, the LCD will begin displaying status information again. Allow several minutes for the software to be copied over and for the upgrade to begin.

## USB Upgrade via CLI

Log into the Local Manager.

Run **config update usb upgrade_filename.bin**. If the filename is not specified, the appliance will attempt to discover this information via the MNF file.

The Local Manager will then copy the file over, verify it, and begin the upgrade.