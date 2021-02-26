<!-- 5.5.2 -->

# Overview

In **5.5.1** and later versions of the UCC, the Uplogix Terminal App can be used to implement the Dial, SSH, and Terminal buttons.


![Uplogix Control Center - Terminal App ](http://uplogix.com/support/docs/img/Uplogix-Terminal-App.jpg)

Users can benefit from the Windows Installer as it decouples the Terminal application from requiring Java on the client's system. The Uplogix Terminal application is a Windows installer that wraps the JNLP (applet) code as an installed Windows application that bundles Java with it. This allows a user to continue running older versions of Java (e.g. 7) for legacy applications and also run the Uplogix Terminal application with the latest supported version of Java that Uplogix bundles with each release.

By default, UCC **v5.5.1** and later will continue to use JNLP and a user will not be required to make any changes. The user has the option to download the Windows Installer and use it with JNLP.


The Windows Terminal application adds several benefits over default JNLP including status icons in the taskbar and a history of recent connections.



The Windows Terminal application is also signed with an EV certificate so that users and Windows can trust the installer is safe.

# Usage

Users can download the Windows Installer (MSI) from their profile page on the UCC.

![Uplogix Control Center - Terminal App Download](http://uplogix.com/support/docs/img/Uplogix-Terminal-App-download.jpg)

Once installed, the terminal app will launch when a JNLP (or UNLP) file is downloaded and opened after clicking the SSH, Dial, or Terminal button on the UCC.

To view your history of recent connections, launch the Terminal App from Windows. Double click on past connections to relaunch the session.

![Uplogix Control Center - Terminal App Download](http://uplogix.com/support/docs/img/Uplogix-Terminal-App-History.jpg)


# UNLP as default terminal launch for all UCC users  

A user with *emsadmin* UCC privileges can change the default terminal launch to Uplogix Network-Launch Protocol (UNLP) for all UCC users by editing embassy.overrides to include TERMINAL_LAUNCH=unlp. This allows the Windows terminal application to automatically associate and launch UNLP files without impacting any file association for JNLP a user may already have.


## Log into the UCC and become root

As with all OS-level configuration, you must first log into the UCC via SSH or console and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root).

## Edit embassy.overrides

Use **vi** to open the /etc/sysconfig/embassy.overrides file.

```
[root@UplogixControlCenter ~]# vi /etc/sysconfig/embassy.overrides
```

Press the "i" key to enter Insert mode. Add the following line to /etc/sysconfig/embassy.overrides:

```
TERMINAL_LAUNCH=unlp
```

Press ESC, then type **:wq** to save the file.

## Restart the UCC

```
[root@UplogixControlCenter ~]# service tomcat restart
```
After the UCC has been restarted the Terminal Launch will show Uplogix Network-Launch Protocol (UNLP) in Administration > Server Settings.


![Uplogix Control Center - Terminal App UNLP Default](http://uplogix.com/support/docs/img/Uplogix-Terminal-App-UNLP-Launch.jpg)