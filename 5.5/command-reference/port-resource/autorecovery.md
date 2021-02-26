<!-- 5.4 -->

Monitors console port activity and determines if the device is in an unresponsive state, cycling the power of the device to recover the device in the least amount of time. The time argument defines the amount of time the console must be unresponsive before the Uplogix Local Manager cycles the power on the device.

This command checks for power control mappings and schedules an intelligentReboot job.

# Command availability

CLI resource: port

Device makes: Cisco

Uplogix Local Managers: All

LMS offerings: All

# Syntax 

```
autorecovery [delay]
```

[delay] is in seconds.

# Usage 

The **autorecovery** command requires power control to function. If there is no power outlet mapped to the device, **autorecovery** will not operate.

```
[admin@UplogixLM (port1/1)]# autorecovery 120
Job was scheduled 9: [Interval: 00:02:00] intelligentReboot
```

# History 

--

# Related commands

--
