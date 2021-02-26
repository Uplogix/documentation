<!-- 5.4 -->

<div class='ucc' />Inventory > Local Manager Summary >Â Network > SNMP</div>

Uplogix Local Managers can report back SNMP information snmp-get or snmp-walk requests. By default, SNMP is disabled. You can enable SNMP with the **config system snmp** command.

**SNMP v3 is required to make requests. Responses are in SNMP v2 format.**

# Available Options

## Security level

Set the security level to disabled to turn off SNMP completely.

The **noAuthNoPriv** level requires that the user connects with the SNMP username, but does no message validation or encryption.

The **authNoPriv** level requires that the user connect with the SNMP username, and makes sure that the message is valid by using the specified auth password.

The **authPriv** level requires that the user connect with the SNMP username, and requires that it has been signed with the Auth password and that it has been encrypted with the Priv password.

Uplogix recommends that you protect the appliance with the authPriv security level.

> Security level designations are case-sensitive.

## Port

You can change the SNMP port from the default of 161.

## Username and passwords

Set a username and the passwords that will be required to execute SNMP requests.

## Auth and Priv protocols

For Auth Protocol, enter SHA or MD5.

For Priv Protocol, enter AES256, AES192, AES128, or DES.

# Enabling SNMP

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

Appliances can be queried using SNMP version 3, which uses usernames in place of community strings. **Note that a version 2 MIB is returned**.

```
admin@support:~$ snmpwalk -u public 172.30.151.100
SNMPv2-MIB::sysDescr.0 = STRING: Envoy UplogixLM1 (A101101474); RMOS build: 20110726:1639214.4.0.20283
SNMPv2-MIB::sysObjectID.0 = OID: SNMPv2-SMI::enterprises.4976
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (17871511) 2 days, 1:38:35.11
SNMPv2-MIB::sysContact.0 = STRING: John Smith
SNMPv2-MIB::sysName.0 = STRING: A101101474
SNMPv2-MIB::sysLocation.0 = STRING: Row12Rack8Slot4
SNMPv2-MIB::sysLocation.0 = No more variables left in this MIB View (It is past the end of the MIB tree)
```

# Viewing SNMP Settings

You can view the current SNMP settings with the **show system snmp** command.

```
[admin@UplogixLM]# show system snmp
Security Level: noAuthNoPriv
Port: 161
Username: public
```