<!-- 5.4 -->

A common issue with network devices is that they become unresponsive. A device console is considered unresponsive when the following three conditions have occurred:

 - The device is powered up.
 - The cable is connected and the serial console is active (i.e., serial handshaking is still occurring).
 - The Local Manager detects that the device's console has been operating for at least four intervals but is no longer responding to requests.

Often the fastest way to recover an unresponsive device is to cycle power.

When used with a supported power controller, the Local Manager can power cycle the device to recover from this state.

> A device (i.e., a router) may stop responding to the console but otherwise remain fully operational. In this situation, power cycling the device may cause unnecessary disruption.

The frozen console recovery feature allows you to set a monitor to check for this condition. The criteria described above, coupled with previously successful polls of the device, trigger a power cycle.

> The Local Manager only power cycles the device once to avoid continuously rebooting the device if the hardware has been damaged.

The device must have a power mapping assigned to it.

To set up autorecovery, navigate to the port of the device to monitor.

```
[admin@UplogixLM]# port 1/2
Quest-HSGS cisco CISCO2911/K9 IOS 15.2(3)T
```

Use the **autorecovery** command to begin the autorecovery monitor.

```
[admin@UplogixLM (port1/2)]# autorecovery 120
Job was scheduled 13: [Interval: 00:02:00] intelligentReboot
The device is now monitored for frozen console.
```