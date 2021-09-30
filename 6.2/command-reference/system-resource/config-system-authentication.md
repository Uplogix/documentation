<!-- 5.4 -->

Interactive command to delegate authentication to external TACACS or RADIUS hosts, or to modify password standards and account lockout for local authentication. To set up authentication for devices connected to the Uplogix Local Manager, use the **config authentication** command.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system authentication
```

# Usage 

Local authentication is updated from TACACS or RADIUS if configured.

If multiple servers are configured and available, the first definitive response is used. An incorrect shared secret responds as invalid authentication.

Uplogix Local Managers do not support challenge-response dialogues.

MSCHAP authentication is only available to Microsoft Windows-based TACACS servers. Account lockout values are only used for local failover if TACACS or RADIUS authentication is selected.

If maximum logins are reached for each user, a message with the currently logged in stations will be presented.

```
[admin@UplogixLM]# config sys authentication
--- Existing  Values ---
Authentication type: local
Limit maximum concurrent sessions: false
Use strong passwords: false
Expire password: false
Number of invalid attempts before lockout: 0
Change these? (y/n) [n]: y
--- Enter New Values ---
Authentication type [local]: tacacs
Authentication method [pap]:
Accounting type [none]: stop-only
Use RADIUS/TACACS Authorization (y/n) [n]: y
Create users (y/n) [n]: y
Cache passwords (y/n) [n]: y
If server is down, should the system use local authentication (y/n) [n]: y
First authentication host IP: 192.168.1.100
First authentication port [0]: 49
First authentication shared secret: *******
Confirm shared secret: *******
Second authentication host IP:
First accounting host IP: 192.165.1.101
First accounting port [0]: 50
First accounting shared secret: *******
Confirm shared secret: *******
Second accounting host IP:
Limit maximum concurrent sessions (y/n) [n]:
Use strong passwords (y/n) [n]: y
Require mixed case (y/n) [n]: y
Require numbers and punctuation (y/n) [n]: y
Reject variation of login id (y/n) [n]: y
Reject word in dictionary (y/n) [n]: y
Reject standard substitutions (@ for a, 3 for e, etc) (y/n) [n]:
Reject sequences in numbers or letters (qwerty) (y/n) [n]: y
Reject previous password (y/n) [n]: y
Number of previous passwords to check [1 to 20] [6]:
Reject single character difference from previous password (y/n) [n]: y
Enforce minimum password length (y/n) [n]: y
Minimum password length [7]:
Expire password (y/n) [n]: y
Number of valid days [30]: 45
Number of invalid attempts before lockout [0]: 3
Lockout duration in minutes [30]: 10
Do you want to commit these changes? (y/n):

```

# In the Uplogix web interface

**Administration > AAA Settings **- applies to the entire inventory

**Inventory > group page > Security > Authentication** - specific to this inventory group

**Inventory > Local Manager page > Security > Authentication** - specific to this system

# History 

3.4 - This command was introduced to replace config Local Manager authentication.

3.5 - Command now allows you to configure separate authentication and accounting servers.

# Related commands 

- **show system authentication**
- **config authentication**
- **show authentication**
 
