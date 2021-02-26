<!-- 5.4 -->

Enabling serial redirection on the Control Center will allow you to access the operating system's command line from the serial port. This is useful if the Control Center is being managed by an Uplogix appliance.

> The steps described below include editing important system files. If you are unsure about editing system files on your Control Center, please contact Uplogix Support for assistance.

## Log in as emsadmin and become root

```
[emsadmin@vUCC-Eval ~]$ sudo su -
[sudo] password for emsadmin:
[root@vUCC-Eval ~]#

```

## Edit /etc/inittab

Add the following line to: /etc/inittab

```
co:2345:respawn:/sbin/agetty ttyS0 9600
```

Other Linux systems may require:

```
7:2345:respawn:/sbin/mingetty ttyS0
```

If there are any other lines in inittab that reference ttyS0, delete them.

Save the file and exit.

## Refresh Init

Run the following command to reload inittab.

```
kill -1 1
```

## Edit /etc/securetty so that root can log in

Add ttyS0 to /etc/securetty

```
[root@ems18 ~]# cat /etc/securetty
console
vc/1
vc/2
vc/3
...
tty10
tty11
ttyS0
```

Save the file and exit.

## Edit the grub configuration file

Add the following to /boot/grub/grub.conf for each line that begins with kernel.

```
console=ttyS0,9600
```

Here is an example grub.conf

```
title Fedora Core (2.6.22.14-72.fc6PAE)
root (hd0,0)
kernel /vmlinuz-2.6.22.14-72.fc6PAE ro root=/dev/VolGroup00/LogVol00 rhgb quiet console=ttyS0,9600
initrd /initrd-2.6.22.14-72.fc6PAE.img
```

## Enable console redirection in BIOS

Restart the Control Center with a keyboard/monitor attached and access the BIOS. Find the tab related to Console Redirection and enable it. Do not enable the feature that says "Redirect console AFTER boot." Post-boot communication will be handled by Linux with the settings above.

## Complete

You should now be able to communicate with your Control Center via the serial port. Please contact Uplogix Support if the above steps do not work.