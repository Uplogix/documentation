<!-- 5.4 -->

In 4.6, available SSH ciphers on the Control Center were restricted to aes128-ctr,aes192-ctr,aes256-ctr.

If you can log into the Control Center via the console, you can update the ciphers to include more options.

1) Gain root access

```
[emsadmin@ems13 ~]$ sudo su -
[root@ems13 ~]#
```

2) Use vi to edit /etc/sysconfig/embassy.overrides.

```
[root@ems13 ~]# vi /etc/sysconfig/embassy.overrides
RAM=4
```

3) Add: SSH_CIPHERS=aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc

```
[root@ems13 ~]# vi /etc/sysconfig/embassy.overrides
RAM=8
SSH_CIPHERS=aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc
```

4) Then run: /uplogix/embassy/scripts/updateSshSettings.sh

```
[root@ems13 ~]# /uplogix/embassy/scripts/updateSshSettings.sh
Stopping sshd: [ OK ]
Starting sshd: [ OK ]
```

5) Try to log in again with SSH