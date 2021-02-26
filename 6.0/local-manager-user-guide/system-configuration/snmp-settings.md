<div class='ucc' />Inventory > Local Manager Summary >Â Network > SNMP</div>

Uplogix Local Managers can report back SNMP information via snmp-get or snmp-walk requests. By default, SNMP is disabled. You can enable SNMP with the **config system snmp** command.

**SNMP v3 is required to make requests. Responses are in SNMP v2 format.**

## Available Options

### Security level

Set the security level to disabled to turn off SNMP completely.

The **noAuthNoPriv** level requires that the user connects with the SNMP username, but does no message validation or encryption.

The **authNoPriv** level requires that the user connect with the SNMP username, and makes sure that the message is valid by using the specified auth password.

The **authPriv** level requires that the user connect with the SNMP username, and requires that it has been signed with the Auth password and that it has been encrypted with the Priv password.

Uplogix recommends that you protect the appliance with the authPriv security level.

> Security level designations are case-sensitive.

### Port

You can change the SNMP port from the default of 161.

### Username and passwords

Set a username and the passwords that will be required to execute SNMP requests.

### Auth and Priv protocols

For Auth Protocol, enter SHA or MD5.

For Priv Protocol, enter AES256, AES192, AES128, or DES.

## Enabling SNMP

For the most secure operation, use AuthPriv:

```
[admin@UplogixLM]# config system snmp
--- Existing Values ---
SNMP is disabled.
Change these? (y/n) [n]: y
--- Enter New Values ---
Security Level (authPriv,authNoPriv,disabled,noAuthNoPriv) [disabled]: authPriv
Port [161]: 
Username: snmpuser
Auth Protocol [SHA]: 
Auth Password: ********
Confirm Auth Password: ********
Priv Protocol [AES256]: 
Priv Password: *********
Confirm Priv Password: *********
Do you want to commit these changes? (y/n): y
```

For quicker access, use the following settings:

```
[admin@UplogixLM]# config system snmp
--- Existing  Values ---
SNMP is disabled.
Change these? (y/n) [n]: y
--- Enter New Values ---
Security Level (authPriv,authNoPriv,disabled,noAuthNoPriv): [disabled]: noAuthNoPriv
Port: [161]:
Username: public
Do you want to commit these changes? (y/n): y
```

Local Managers can be queried using SNMP version 3, which uses usernames in place of community strings. **Note that a version 2 MIB is returned**.

```
admin@support:~$ snmpwalk -u public 10.10.10.24
iso.3.6.1.2.1.1.1.0 = STRING: "Envoy UplogixLM (A505100584); LMS build: 20200211:041628 6.0.0.35585"
iso.3.6.1.2.1.1.2.0 = OID: iso.3.6.1.4.1.10243
iso.3.6.1.2.1.1.3.0 = Timeticks: (8319559) 23:06:35.59
iso.3.6.1.2.1.1.4.0 = ""
iso.3.6.1.2.1.1.5.0 = STRING: "UplogixLM"
iso.3.6.1.2.1.1.6.0 = ""
iso.3.6.1.2.1.25.2.3.1.1.1 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.1.3 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.1.31 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.2.1 = OID: ccitt.0
iso.3.6.1.2.1.25.2.3.1.2.3 = OID: ccitt.0
iso.3.6.1.2.1.25.2.3.1.2.31 = OID: ccitt.0
iso.3.6.1.2.1.25.2.3.1.3.1 = ""
iso.3.6.1.2.1.25.2.3.1.3.3 = ""
iso.3.6.1.2.1.25.2.3.1.3.31 = ""
iso.3.6.1.2.1.25.2.3.1.4.1 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.4.3 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.4.31 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.5.1 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.5.3 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.5.31 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.6.1 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.6.3 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.6.31 = INTEGER: 0
iso.3.6.1.2.1.25.2.3.1.7.1 = Counter32: 0
iso.3.6.1.2.1.25.2.3.1.7.3 = Counter32: 0
iso.3.6.1.2.1.25.2.3.1.7.31 = Counter32: 0
```

## Viewing SNMP Settings

You can view the current SNMP settings with the **show system snmp** command.

```
[admin@UplogixLM]# show system snmp
Security Level: noAuthNoPriv
Port: 161
Username: public
```