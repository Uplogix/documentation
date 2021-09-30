<!-- 5.4 -->

Displays the Uplogix Local Manager's inbound connectivity configuration, including Telnet, SSH, IP address filtering, and DHCP base address. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 
```
show system protocols [-s]
```

**-s** - displays filter statistics

# Usage 
Protocol changes take effect after restart. This command shows the current settings; however, if the system has not been restarted, the settings may not be in effect.

```
[admin@UplogixLM]# show system protocols
Telnet: disabled
Server DHCP base address: 169.254.100
sshPort: 22
Preferred Encryption Cipher:3des-cbc
Allow: aes128-cbc
Allow: aes128-ctr
Allow: aes192-cbc
Allow: aes192-ctr
Allow: aes256-cbc
Allow: aes256-ctr
Allow: blowfish-cbc
Allow: cast128-cbc
Allow: twofish128-cbc
Allow: twofish192-cbc
Allow: twofish256-cbc
Preferred HMAC:hmac-sha1
Allow: hmac-md5
Preferred Compression:none
Allow: zlib
Preferred Key Exchange Algorithm:diffie-hellman-group1-sha1
Allow: diffie-hellman-group14-sha1
```

# In the Uplogix web interface

**Inventory > group page > Network > Protocols** - specific to this inventory group

**Inventory > Local Manager page > Network > Protocols** - specific to this system

# History 

3.4 - This command was introduced to replace show envoy protocols. DHCP information was added.

3.5 - Command output was expanded to show configurable ssh options.

# Related commands 

- **config system protocols dhcp**
- **config system protocols filter**
- **config system protocols ssh**
- **config system protocols telnet**
