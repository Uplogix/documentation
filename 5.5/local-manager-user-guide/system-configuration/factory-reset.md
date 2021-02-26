<!-- 5.4 -->

# Overview

In some situations, you may wish to clear all configuration information, logs, and other data stored on the Local Manager. Factory reset completes the following:

- shuts down all services
- reformats the hard drive
- reinstalls the software

**No data is retained.** Following a factory reset, the Local Manager is in its initial state, just as it was when it was shipped. However, it will remain on its current software revision if it has been upgraded since its purchase.

> To set an individual port back to its initial state, use the **config system clear port** command.

<div class='warning'>Do not power off or cycle power during the factory reset process.</div>

If the Local Manager is managed by a Control Center, delete it from the inventory before starting the factory reset.

Following a factory reset, the Local Manager will need to be reconfigured.

# Factory Resetting a Local Manager via the CLI 

Local Managers can be factory reset using the **config reinstall** command. To protect against accidental usage, this command is not included in any of the default roles. It must be added to the role of the user. In this example, we will create a new role and assign it to the admin user.

1)  Create a role called reinstall.

```
[admin@UplogixLM]# config role reinstall
Role reinstall does not exist. Create (y/n): y
```

2)  Add the config reinstall permission to the role.

```
[config role reinstall]# allow config reinstall
[config role reinstall]# exit
```

3)  Edit the admin user and assign the reinstall role on the system resource.

```
[admin@UplogixLM]# config user admin
[config user admin]# system reinstall
[config user admin]# exit
```
4)  Admin can now run the **config reinstall** command.

```
[admin@UplogixLM]# config reinstall
** Issuing this command will completely reset the system. **
** All data will be lost. IP connectivity will be lost. **
Proceed? (y/n): y
```

> If the Local Manager is managed by a Control Center, role creation and assignment will need to be done on the Control Center.

# Factory Resetting an Uplogix 400, 3200, or 5000 via the Keypad

A factory reset can be initiated if you have physical access to the Local Manager keypad. To do so:

1. Press then center button on the keypad to enter the menu.
2. Scroll down to *Factory Reset*, press the center button to select it. **You will have to scroll down past two blank lines.**
3. Confirm your decision to Factory Reset.

By default, the Local Manager will try to acquire an IP address via DHCP, so you will have to readdress the device once it finishes.

# Factory Resetting an Uplogix 500 Local Manager

1. Shut down the device, either using the **shutdown** command or by pressing and releasing the power cycle button.
2. Press and HOLD the Multi-function Button (the button with a checkmark next to it). At the same time press and release the Power button.
3. The Status LED will change from OFF -> SLOW BLINK -> FAST BLINK.
4. Once the Status LED changes to FAST BLINK you may release the Multi-Function button and the Factory Reset will begin.
5. During the Factory Reset, the Status LED will change to SLOW BLINK and remain in that state until the Factory Reset is complete.

> You can connect to the console port of the Uplogix 500 and watch the factory reset process.

# Factory Resetting an Uplogix 430 Local Manager

> Read through the instructions completely before attempting to factory reset your device.

1. Shut down the device, either using the **shutdown** command or by pressing the power cycle button and holding it for five seconds.
2. Disconnect the power cable.
3. Press and HOLD the power button.
4. Connect the power cable.
5. The system health light will change from OFF -> SLOW BLINK -> FAST BLINK as the device boots up.
6. When the system health light changes to FAST BLINK, release the power button.
7. Immediately press and HOLD the power button again until the system health light turns off.

Release the power button when the system health light turns off.

> You can connect to the console port of the Uplogix 430 and watch the factory reset process.

If you do not complete the sequence of button presses, the device will boot normally.