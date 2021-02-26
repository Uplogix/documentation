<!-- 5.4 -->

# Disk Usage

You can get an overview of the disk usage on a Local Manager by running the **show directory** command from the system resource.

```
[admin@UplogixLM]# show directory
port1/1: 0 bytes in 0 files.
port1/2: 5.6 MB in 9 files.
port1/3: 0 bytes in 0 files.
port1/4: 0 bytes in 0 files.
 20.0 GB free (99%)
```

# Set CLI Page Length

By default, the Local Manager automatically determines the appropriate number of lines to display in the CLI window before providing a scroll prompt. If the appropriate page length cannot be determined, the CLI displays 24 lines before presenting a scroll prompt.

To change the number of lines displayed, use the **config system page-length** command:

```
[admin@UplogixLM]# config system page-length
Page length preference is auto.
Change this? (y/n) [n]: y
Page length preference (2 or more lines or auto):15
```

In this example, the command line will display 15 lines before prompting you to press a key to scroll the display.

# Set Console Null Modem

> **Deprecated.** This command is not available on the Uplogix 500/5000.

Default management console connection settings are 9600 baud, 8 data bits, 1 stop bit, no parity, and no flow control.

**NOTE:** By default, Windows HyperTerminal uses hardware flow control. The Uplogix 430 does not use flow control. If you use HyperTerminal with the Uplogix 430, you must disable flow control when configuring the session.

The Uplogix 3200 accepts standard RS-232 serial cables with RJ-45 connectors, but can be configured to use null modem cables instead.

The Uplogix 430 is shipped with its own console cable. You do not need to enable null modem on the Uplogix 430.

To use a null modem cable, use the interactive **config system serial** command and enable the null modem setting, if it was not enabled during initial configuration.

```
[admin@Uplogix3200]# config system serial
--- Existing Values ---
Null modem: no
Change these? (y/n) [n]: y
Enable null modem? (y/n) [n]: y
Do you want to commit these changes? (y/n): y
```