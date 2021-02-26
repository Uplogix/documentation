<!-- 5.4 -->

Configures the Uplogix Local Manager to listen to SSH requests on a TCP port other than the default port 22, and sets the preferred and allowed encryption types.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system protocols ssh <22 | {1024..10000}>
```

# Usage 

This change requires a reboot of the system to take effect.

```
[admin@UplogixLM]# config system protocols ssh
--- Existing  Values ---
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
Change these? (y/n) [n]: 
```

# In the Uplogix web interface

**Inventory > group page > Network > Protocols > SSH** - specific to this inventory group

**Inventory > Local Manager page > Network > Protocols > SSH** - specific to this system

# History 

3.4 - This command was introduced

3.5 - Configurable encryption added.

# Related commands 

- **show system protocols**
