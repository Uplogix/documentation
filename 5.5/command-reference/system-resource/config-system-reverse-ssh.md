<!-- 5.4 -->

Initiates a reverse SSH connection from the Local Manager to the Control Center.   

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All


# Syntax

```
config system reverse-ssh
```

# Usage

```
[admin@UplogixLM]# config system reverse-ssh
--- Existing  Values ---
Enabled: false
Change these? (y/n) [n]: y
--- Enter New Values ---
Enabled (y/n) [n]: y
Limit SSH login to RSSH only (y/n) [n]:
Reverse SSH server port [2222]:
SSH keep-alive seconds [90]:
SSH keep-alive bytes [32]:
Do you want to commit these changes? (y/n): y
generating rsa ssh certificate (rev-ssh)
Generating 2048-bit RSA key pair.
```

# In the Uplogix web interface

**Inventory > group page > Network > Reverse SSH** - specific to this inventory group

**Inventory > Local Manager page > Network > Reverse SSH** - specific to this system

# Related Commands

- **show system reverse-ssh**