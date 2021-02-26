This command resets a Local Manager to factory configuration. 

To set an individual port back to its initial state, use the **config system clear port** command.

Do not power off or cycle power during the factory reset process.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All
# Syntax

```
config reinstall
```

# Usage

> **Note**: To protect against accidental usage, this command is not included in any of the default roles. It must be added to the role of the user.

1) Create a role called reinstall.

```
[admin@UplogixLM]# config role reinstall
Role reinstall does not exist. Create (y/n): y
```

2) Add the config reinstall permission to the role.

```
[config role reinstall]# allow config reinstall
[config role reinstall]# exit
```

3) Edit the admin user and assign the reinstall role on the system resource.

```
[admin@UplogixLM]# config user admin
[config user admin]# system reinstall
[config user admin]# exit
```
4) Admin can now run the config reinstall command.

```
[admin@UplogixLM]# config reinstall
** Issuing this command will completely reset the system. **
** All data will be lost. IP connectivity will be lost. **
Proceed? (y/n): y
```

If the Local Manager is managed by a Control Center, role creation and assignment will need to be done on the Control Center.

# Related commands 

- **restart**
- **shutdown**