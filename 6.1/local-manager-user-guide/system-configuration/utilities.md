There are a few utilities in LMS 6.0 that may be useful during everyday use.

## View Disk Usage

You can get an overview of the disk usage on a Local Manager by running the **show directory** command from the system resource.

```
[admin@UplogixLM]# show directory
port1/1: 0 bytes in 0 files.
port1/2: 51.7 MB in 11 files.
port1/3: 141.7 KB in 19 files.
port1/4: 0 bytes in 0 files.
port1/5: 0 bytes in 0 files.
port1/6: 0 bytes in 0 files.
port2/1: 2.1 KB in 1 files.
port2/2: 0 bytes in 0 files.
port2/3: 421.6 MB in 29 files.
port2/4: 421.5 MB in 19 files.
port2/5: 28.3 MB in 35 files.
port2/6: 0 bytes in 0 files.
port2/7: 0 bytes in 0 files.
port2/8: 0 bytes in 0 files.
port4/1: 0 bytes in 0 files.
port4/2: 0 bytes in 0 files.
  19.1 GB free (95%)
```

## Set CLI Page Length

By default, the Local Manager automatically determines the appropriate number of lines to display in the CLI window before providing a scroll prompt. If the appropriate page length cannot be determined, the CLI displays 24 lines before presenting a scroll prompt.

To change the number of lines displayed, use the **config system page-length** command:

```
[admin@UplogixLM]# config system page-length
Page length preference is auto.
Change this? (y/n) [n]: y
Page length preference (2 or more lines or auto):15
```

In this example, the command line will display 15 lines before prompting you to press a key to scroll the display.