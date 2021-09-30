# Overview

For the best and most secure experience, Uplogix Local Managers should always run the latest version of LMS. Uplogix generally releases two new versions of software each year, but may also release patches if important bugfixes or security updates are required.

To ensure proper operation of the Local Manager with the Control Center, both need to be running the same minor revision of software. That is, **the first two numbers of the version** need to be the same.

For example, a 6.0.0 Local Manager will work fine with a 6.0.1 Control Center. A 5.5 Local Manager, however, will not synchronize with a 6.0.x Control Center.

# About the Upgrade

Here's what happens when you upgrade a Local Manager:

1. The bin file is downloaded to the Local Manager
2. The bin file is decrypted and verified
3. Upgrade files are unpacked onto the filesystem
4. The Local Manager restarts to perform the upgrade.

The Local Manager will be available until Step 4. During the upgrade, the operating system will be up and responding to pings, but SSH will be unavailable until the upgrade is complete.

# Choosing the Right Software
Uplogix provides three different versions of each LMS release.

* Standard
* Government (FIPS) - denoted with a **g** in the filename
* Virtual

Virtual software is used for the initial deployment of Virtual Local Managers. After initial deployment, VLMs can be upgraded as if they were regular hardware Local Managers.

For standard deployments, consult the chart below:

| | Version 5.5 or earlier | 6.0 or later |
| - | - | - |
| Uplogix LM80/LM83X | **not supported** | UplogixOS-6.0.X-YYYYY.bin |
| Uplogix 500/5000 | UplogixOS-6.0.X.YYYYY-500-5000.bin | UplogixOS-6.0.X-YYYYY.bin |

For FIPS 140-2 compliant deployments, consult the chart below:

| | Version 5.5 or earlier | 6.0 or later |
| - | - | - |
| Uplogix LM80/LM83X | **not supported** | UplogixOS-6.0.X-YYYYYg.bin |
| Uplogix 500/5000 | UplogixOS-6.0.X.YYYYYg-500-5000.bin | UplogixOS-6.0.X-YYYYYg.bin |

Previous EOL platforms are no longer supported and cannot be upgraded.
# Download Software

Visit your Uplogix Support Site account page at uplogix.com/support/account.

<div class='warning' />An active maintenance contract is required to access the Uplogix Support Site account page and/or download software. If your maintenance contract has expired, please contact Uplogix Support.</div>

Find the green button marked *Download Software*.

![Support Site Software Downloads](http://uplogix.com/support/docs/img/6.0/downloads-main.png)

Click the folder link for your desired software version.

![Support Site Download Link](http://uplogix.com/support/docs/img/6.0/downloads-directory.png)

Click the link to download the bin file to your desktop.

<div class='danger'>Uplogix 500/5000 Local Managers running 5.5 or earlier must download the bin file tagged with '500-5000'.</div>

<div class='warning'>The latest version of software (**6.0**) will not run on EOL Local Managers, including the Uplogix 400, 430, and 3200.</div>

> Customers with Local Managers on older versions (**5.3.0** or older) will need to upgrade in steps to get to 6.0.2 (first to **5.4.3**, then again to **6.0.2**). Please contact Uplogix Support for information on your upgrade path and what files are needed prior to the upgrade.


# Upgrading via SCP, FTP, and HTTP

SCP, FTP, and HTTP require the lms.bin file to be staged on an appropriate server. Push the file to an SCP, FTP, or HTTP server.

> The Control Center can be used as an SCP target because of its Linux operation system. Use a program like WinSCP or pscp to transfer the bin file to /home/emsadmin.

<div class='danger' />While possible, please do not use the Uplogix Support Site as an HTTP target if you upgrade a large number of Local Managers.</div>

Log into your Local Manager and use the **config update** command to initiate the upgrade. You will need to specify the IP address or hostname of the target and the path to the file.

For example:

```
config update scp user@198.51.100.172:UplogixOS-6.0.1.36252.bin
```

or


```
config update ftp user@198.51.100.172:UplogixOS-6.0.1.36252.bin
```

or

```
config update http http://198.51.100.172/UplogixOS-6.0.1.36252.bin
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