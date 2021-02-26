Proper configuration of a Cisco router will allow it to fail over to local authentication if the connection to TACACS fails. However, a situation can occur where the connection fails after the user is successfully authenticated. This may prevent the user (e.g. the Uplogix Local Manager) from performing basic commands such as logout.

To account for this situation, modify the aaa statements in the config of your Cisco router.

# Example Cisco Router Config

```
aaa authentication login default group tacacs+ local
aaa authorization console
aaa authorization exec default local group tacacs+
aaa authorization commands 0 default local group tacacs+ if-authenticated
aaa authorization commands 1 default local group tacacs+
aaa authorization commands 15 default local group tacacs+
```

Adding the argument **if-authenticated** will allow a user to execute level 0 commands even if the connection to TACACS is lost after authentication. This will allow the Local Manager to log out of the Cisco router so that local authentication can be used.

The **if-authenticated** argument can be added to the other command levels if desired.

# Example Cisco ACS Settings

1. Create a user
2. Configure PAP and CHAP passwords
3. Under Advanced TACACS+ Settings, set Max Privilege for Clients to "Level 15" via the drop-down menu
4. View TACACS+ Enable Password settings.
	1. If it matches the enable password on the device, the user will be taken directly to the # prompt.
	2. If it doesn't match, or if you use "Cisco Secure PAP Password," the user will be given the > prompt and will need to enter the device's enable password at the device prompt.
5. Set TACACS+ Outbound Password to what you entered for PAP and CHAP
8. Under TACACS+ Settings, check "Shell EXEC" and set Privilege Level to 15.
9. Under Shell Command Authorization, assign a set of Full Access. This set may need to be created beforehand.

# Creating an ACS Command Authorization Set

1. Within ACS, click on Shared Profile Components button.
2. Click on Shell Command Authorization Sets.
3. Click on an existing set name to edit or click Add to create a new set.
4. In the entry window, add commands you wish to allow. You can also choose to deny execution of all commands not included in the entry window.