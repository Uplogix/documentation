<!-- 5.4 -->

Interactive command to activate or deactivate basic SNMP settings. SNMP may be disabled, or set to one of the following security levels: 

**noAuthNoPriv** security requires that the user connects with the SNMP username, but does no message validation or encryption. 

**authNoPriv** security requires that the user connect with the SNMP username, and makes sure that the message is valid by using the specified auth password. 

**authPriv** security requires that the user connect with the SNMP username, that it has been signed with the Auth password and that it has been encrypted with the Priv password. 

For security, Uplogix recommends using the authPriv security level. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system snmp
```

# Usage 

```
[admin@UplogixLM]# config system snmp
--- Existing  Values ---
SNMP is disabled.
Change these? (y/n) [n]: y
--- Enter New Values ---
Security Level (authPriv,authNoPriv,noAuthNoPriv,disabled): [disabled]: authPriv
Port: [161]:
Username: xyzcoAus01
Auth Protocol: [SHA]:
Auth Password: *********
Confirm Auth Password: *********
Priv Protocol: [AES256]:
Priv Password: *********
Confirm Priv Password: *********
Do you want to commit these changes? (y/n): y
```

Auth protocol may be set to SHA (default) or MD5. Priv protocol may be set to AES256 (default), AES192, AES128, or DES. 

You will only be prompted for the applicable passwords.

> **Note**: You can set appropriate values for sysContact.0 and sysLocation.0 with the **config system properties** command. 

To disable SNMP, set the security level to disabled.


```
[admin@UplogixLM]# config system snmp
--- Existing  Values ---
Security Level: authPriv
Port: 161
Username: xyzcoaus01
Auth Protocol: SHA
Auth Password: ********
Priv Protocol: AES256
Priv Password: ********
Change these? (y/n) [n]: y
--- Enter New Values ---
Security Level (authPriv,authNoPriv,noAuthNoPriv,disabled): [authPriv]: disabled
Do you want to commit these changes? (y/n): y
```

# In the Uplogix web interface

**Inventory > group page > Network > SNMP** - specific to this inventory group

**Inventory > Local Manager page > Network > SNMP** - specific to this system

# History 

3.4 - This command was introduced to replace config envoy snmp.

# Related commands 

- **show system snmp**
