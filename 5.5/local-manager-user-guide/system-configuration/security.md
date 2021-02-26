<!-- 5.4 -->

# AAA Settings

For a discussion of the **config system authentication** command, see [Managing Authentication Settings](http://uplogix.com/docs/local-manager-user-guide/managing-user-accounts/managing-authentication-settings)

# Keypad Lockout

<div class='ucc' />Inventory > Local Manager Summary >Â System > LCD</div>

After completing basic configuration, you may choose to disable the front panel keypad using the **config system keypad** command. This prevents configuration changes from the keypad. The restart, shutdown, and factory reset functions remain available from the keypad at all times. 

```
[admin@UplogixLM]# config system keypad disable
Keypad Configuration: disabled

[admin@UplogixLM]# config system keypad enable 
Keypad Configuration: enabled
```

# LCD Information

<div class='ucc' />Inventory > Local Manager Summary >Â System > LCD</div>

By default, the Local Manager displays status information on the front LCD panel. You can disable this display with the **config system lcd** command.

```
[admin@UplogixLM]# config system lcd disable
Display system information on the LCD: disabled
```

The LCD will still display menu options when buttons are pressed, but will be blank otherwise.