<!-- 5.4 -->

> The Uplogix Documentation Team is currently working on expanding this topic, so check back for more updates later!

# Security Policy

The Uplogix Local Manager can be operated in a secure manner that complies with FIPS 140-2 for customers whose corporate security policy requires it. The latest FIPS Security Policy document is available [here](/docs/pdf/Uplogix%20FIPS%20Security%20Policy%204.6.pdf).
 
# Enabling FIPS Mode

To enable FIPS mode, the Local Manager must be running the **-g** version of LMS software. On the [Software Downloads](/support/account/) page, two files are available for the Local Manager: lms.bin and lms-g.bin. Download and upgrade to the **G** version before continuing.

```
[admin@UplogixLM]# config update scp software@fileserver:software/envoy6.0/lms-g.bin
** Issuing this command will restart the system. ** 
Proceed? (y/n): y
```

You can use the **show version** command to verify your version.

```
[super@UplogixLM]# show ver

Model: Uplogix LM83x
Serial number: A123456789
LMS version: 6.0.0.35619g
LMS build: 20200221:041342
FIPS 140-2 mode: disabled
Slot 2 serial number: 
Slot 3 serial number: 
Slot 4 serial number: AM1229170029
```

For LMS version, the number should end in a **g**.

To enable FIPS mode, use the **config system fips enable** command. A strong warning will be presented.

```
[super@UplogixLM]# config system fips enable
** Issuing this command disables services and cryptographic algorithms to **
** comply with FIPS 140-2 rules and the Uplogix security policy.          **
**                                                                        **
** New SSH host keys will be generated.                                   **
**                                                                        **
** This system will not be able to talk to the management server,         **
** unless the management server is also running in FIPS mode.             **
**                                                                        **
** The system will reboot after changing its configuration.               **
**                                                                        **
** This process can only be undone with a factory reset which will result **
** in all data being lost.                                                **
**                                                                        **
** THIS PROCESS IS IRREVERSIBLE.                                          **

Proceed? (y/n) [n]: y
Enter your password to confirm: 
```

Once you confirm the operation and enter your password, the Local Manager will enable FIPS and reboot.

```
Verifying system integrity...
...................................
Updating configuration...
Clearing heartbeat certificates...
Clearing SSH host keys...
Clearing secure dial-in keys and certificate...
Clearing virtual-port SSH keys...
Clearing SMS key...
Restarting...
Connection to 198.51.100.26 closed by remote host.
Connection to 198.51.100.26 closed.
```

After the reboot, verify FIPS mode is enabled with the **show version** command.

```
[admin@UplogixLM]# show ver
All Rights Reserved. Uplogix and its respective logos are trademarks of Uplogix, Inc. in the United States and other
jurisdictions. This product is protected by U.S Patent 7,512,677 and other patents pending. The programs included herein are
subject to a restricted use license and can only be used in conjunction with this application.

Model: Uplogix LM83x
Serial number: A700000115
LMS version: 6.0.0.35619
LMS build: 20200221:041342
FIPS 140-2 mode: enabled
Slot 2 serial number: 
Slot 3 serial number: 
Slot 4 serial number: AM1229170029
```

FIPS mode is now enabled.

