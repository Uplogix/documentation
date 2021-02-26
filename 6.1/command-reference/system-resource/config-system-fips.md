<!-- 5.4 -->

Interactive command to set the Local Manager into FIPS mode.  In FIPS mode the Local Manager can only be managed with a FIPS configured Control Center.

See the Uplogix FIPS 140-2 Security Policy Guide for additional reference.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system fips enable
```

# Usage 

This change zeros all keys and regenerates ssh key pairs.  

> **Note: THIS PROCESS IS NOT REVERSIBLE**.                                          

```
[admin@UplogixLM]# config system fips enable

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

Proceed? (y/n) [n]:y
<output removed>
```

# History 

4.3 - This command was introduced.

# Related commands 

- **show system fips**
