<div class='ucc' />Inventory > Local Manager (or Group) Summary Page > System > LCD</div>

# Keypad Lockout
After completing basic configuration, you may choose to disable the front panel keypad using the **config system keypad** command. This prevents configuration changes from the keypad. The restart, shutdown, and factory reset functions remain available from the keypad at all times.

```
[admin@UplogixLM]# config system keypad disable
Allow system configuration from the keypad: disabled

[admin@UplogixLM]# config system keypad enable
Allow system configuration from the keypad: enabled
```

# LCD Information

By default, the Local Manager displays status information on the front LCD panel. You can disable this display with the **config system lcd** command.

```
[admin@UplogixLM]# config system lcd disable
Display system information on the LCD: disabled

[admin@UplogixLM]# config system lcd enable
Display system information on the LCD: enabled
```

When disabled, LCD will still display menu options when buttons are pressed, but will be blank otherwise.