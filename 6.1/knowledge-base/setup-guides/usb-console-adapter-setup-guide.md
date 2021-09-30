# Overview

The USB Console Adapter was designed to overcome the lack of a dedicated RS-232 console port on newer network devices. It is typically installed between the Local Manager and a network device, providing an RS-232 RJ-45 interface on one side and a USB interface on the other. Installation and operation are simple, requiring only two connections plus power.

# Unpacking the box

The following items are included in the box:

* USB Console Adapter with Micro-USB Type B, RJ-45, and USB-A interface ports
* Universal power adapters with Micro-USB Type B power connector

# Required items

* RJ-45 Straight-through patch cable
* **Vendor-provided** USB console cable

# Installation

Use the following diagram and the instructions below to install the USB Console Adapter.

> <b>NOTE:</b> Only the *native* and *enhanced native* drivers are supported with the USB Console Adapter. Advanced drivers are not currently available.

![USB Console Adapter Installation Diagram](https://uplogix.com/support/docs/img/6.1/usb_console_adapter_install_diagram.jpg)

1) Connect an RJ-45 straight-through patch cable to the appropriate port on the Local Manager

2) Connect the other end of the patch cable to the RJ-45 port on the USB Console Adapter.

3) Connect a USB cable's USB-A interface to the USB-A port on the USB Console Adapter.

4) Connect the USB cable to the network device to be managed.

5) Connect the Micro-USB Type B power connector from the included power supply to the USB Console Adapter. The Micro-USB Type B port is marked *POWER*.

6) Plug the power supply into an active outlet.

7) Observe the LED status light next to the USB-A port on the USB Console Adapter.

# LED Status Lights

* GREEN - device is powered
* RED - booting or error
* BLUE - device plugged in and active (normal operating state)

# Test the connection

Once you have a BLUE light on the USB Console Adapter, you should be able to test serial communication from the Local Manager. Log into the Local Manager, navigate to the appropriate port, and use the **terminal** command to verify connectivity.

If you cannot communicate with the device, check all connections and ensure baud rate settings are correct. If you continue to encounter issues, please contact Uplogix Support.

# Setup complete

The USB Console Adapter does not require any further configuration. If power is lost, the connection will drop. Communication will resume when power is restored.

