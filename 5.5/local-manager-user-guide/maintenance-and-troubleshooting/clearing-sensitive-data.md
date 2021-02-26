<!-- 5.4 -->

In some deployments, it may be necessary to clear the Local Manager's hard drive prior to decommissioning or before it is returned to Uplogix for replacement. To perform this operation, you will need admin access to the system. If you cannot access the CLI or boot the LM, the hard drive will need to be removed prior to return to Uplogix.

* [Uplogix 5000 Hard Drive Removal](/docs/local-manager-user-guide/maintenance-and-troubleshooting/u5000-hard-drive-removal)
* [Uplogix 500 Hard Drive Removal](/docs/local-manager-user-guide/maintenance-and-troubleshooting/u500-hard-drive-removal)
* [Uplogix 3200 Hard Drive Removal](/docs/local-manager-user-guide/maintenance-and-troubleshooting/u3200-hard-drive-removal)

# FIPS 140-2 Mode

FIPS 140-2 ([Federal Information Processing Standard](https://en.wikipedia.org/wiki/FIPS_140-2)) mode is an elevated security model used by the Uplogix Local Manager in high security deployments. Due to the strong security requirements, performing a factory reset while in FIPS mode will:

* Reformat the hard drive
* Crypto scramble SSDs
* Zero-out spinning disks

All data will be securely erased from the system.

To check whether your LM is running in FIPS mode, use the **show version** command.

```
[super@UplogixLM]# show version | grep FIPS
FIPS 140-2 mode: disabled
```

If you are not running FIPS mode, enable it with the **config system fips enable** command.

> A **g** version of LMS software is not required to put a Local Manager into FIPS mode. However, customers using FIPS mode on a daily basis should only run it on a **g** build. For more information, please contact Uplogix Support.

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

Proceed? (y/n) [n]: 
```

Once the LM has rebooted, verify FIPS mode with the **show version** command.

```
[super@UplogixLM]# show version | grep FIPS
FIPS 140-2 mode: enabled
```

# Factory Reset

Once the LM is running in FIPS mode, you can proceed with the factory reset.

* [Factory Reset](/docs/local-manager-user-guide/system-configuration/factory-reset)