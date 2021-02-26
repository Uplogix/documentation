<!-- 5.4 -->

Displays the Uplogix Local Managerâ€™s inbound connectivity configuration, including Telnet, SSH, IP address filtering, and DHCP base address. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 
```
show system protocols [-s]
```

**-s** â€“ displays filter statistics

# Usage 
Protocol changes take effect after restart. This command shows the current settings; however, if the system has not been restarted, the settings may not be in effect.

```
[admin@UplogixLM]# show system protocols
Telnet: disabled
Server DHCP base address: 192.168.1
sshPort: 22
Preferred Encryption Cipher:aes128-ctr
Allow: aes128-cbc
Allow: aes128-gcm@openssh.com
Allow: aes192-cbc
Allow: aes192-ctr
Allow: aes256-cbc
Allow: aes256-ctr
Allow: aes256-gcm@openssh.com
Allow: twofish128-cbc
Allow: twofish192-cbc
Allow: twofish256-cbc
Preferred HMAC:hmac-sha2-256
Allow: hmac-sha1
Allow: hmac-sha2-512
Preferred Compression:none
Allow: zlib
Preferred Key Exchange Algorithm:diffie-hellman-group14-sha1
Allow: diffie-hellman-group-exchange-sha1
Allow: diffie-hellman-group-exchange-sha256
Allow: diffie-hellman-group1-sha1
Allow: ecdh-sha2-nistp256
Allow: ecdh-sha2-nistp384
Allow: ecdh-sha2-nistp521
deny 192.0.2.1
deny 198.51.100.0/24
```

# In the Uplogix web interface

**Inventory > group page > Network > Protocols** - specific to this inventory group

**Inventory > Local Manager page > Network > Protocols** - specific to this system

# History 

3.4 - This command was introduced to replace show envoy protocols. DHCP information was added.

3.5 â€“ Command output was expanded to show configurable ssh options.

# Related commands 

- **config system protocols dhcp**
- **config system protocols filter**
- **config system protocols ssh**
- **config system protocols telnet**
