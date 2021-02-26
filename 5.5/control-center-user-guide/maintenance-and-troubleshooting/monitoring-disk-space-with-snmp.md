<!-- 5.4 -->

# Overview

SNMP can be configured on the Control Center to monitor disk space and send an alert if space is getting low. A full disk partition may cause the UCC to stop responding to HTTPS requests.

# Install RPMs (version 5.3 and lower)

Log into the UCC as emsadmin and become root.

```
[djones@centos-vm ~]$ ssh emsadmin@uplogix-cc
emsadmin@uplogix-cc's password: 
[emsadmin@UplogixControlCenter ~]$ sudo su -
[sudo] password for emsadmin: 
[root@UplogixControlCenter ~]# 
```

Versions 5.3 and lower require additional RPMs to enable this feature. Log into the [Uplogix Support Site](/support/account/) and download the **cc-rpms.tar** file for version 5.3. Transfer the tar file to the UCC.

> If your UCC can reach uplogix.com, you can use wget to pull the file directly to the UCC.

Untar the file:

```
[root@UplogixControlCenter ~]tar -xvf cc-rpms5.3.tar
freeradius-1.1.8-uplogix.6.el5.i386.rpm
net-snmp-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm
net-snmp-libs-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm
net-snmp-uplogix-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm
net-snmp-utils-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm
openjdk-8-jre-1.8.0_40b25-uplogix.4.i386.rpm
osUpdates5-5.3-uplogix.12.el5.i386.rpm
safenet-3.0.0-8.uplogix.2.i386.rpm
tomcat-6.0.44-uplogix.2.i386.rpm
uplogix-nss-3.12.11-safenet.uplogix.14.el5.i386.rpm
uplogix-nss-3.12.11-uplogix.14.el5.i386.rpm
xinetd-2.3.14-20.el5_10.uplogix.2.i386.rpm
```

Install the relevant RPMs:

```
[root@UplogixControlCenter ~] rpm -Uvh net-snmp-libs-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm
Preparing...                ########################################### [100%]
   1:net-snmp-libs          ########################################### [100%]

[root@UplogixControlCenter ~]# rpm -Uvh net-snmp-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm  
Preparing...                ########################################### [100%]
   1:net-snmp               ########################################### [100%]

[root@UplogixControlCenter ~]# rpm -Uvh net-snmp-utils-5.3.2.2-25.el5_11.uplogix.1.el5.i386.rpm
Preparing...                ########################################### [100%]
   1:net-snmp-utils         ########################################### [100%]
```

# Configure SNMP

Edit the snmpd.conf and add the following information:

```
[root@UplogixControlCenter ~]# vi /etc/snmp/snmpd.conf
```

Ensure these components are present. There may already be configuration information present, and more may be added to monitor other aspects of the UCC.

```
com2sec notConfigUser  default [public or community]

trapcommunity [public or community] 
trap2sink [127.0.0.1 - or IP address of SNMP receiver]

syslocation UplogixInNoc
syscontact CustomerName <root@localhost>

agentSecName notConfigUser
rouser notConfigUser

disk / 30%
disk /u00 10%
disk /u01 10%
disk /u02 10%
disk /u03 10%
disk /u04 30%
disk /u05 30%

monitor -r 60 -o dskPath -o dskErrorMsg "UplogixCC Disk Warning"  dskErrorFlag  != 0
```

# Enable SNMP to Run at Startup

Now that you have configured snmpd, you will need to ensure that it is
running on startup by executing the following commands as root:

```
service snmpd start
chkconfig --level 345 snmpd on
```

# Setup Complete

You will now start receiving SNMP traps at your trap receiver whenever the disk space is running low.  To change the thresholds for these traps, you may edit snmpd.conf.  

> u00-u03 are sparse database files, they should not grow.