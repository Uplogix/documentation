<!-- 5.4 -->

Interactive command to set the number of lines displayed in the CLI window before you are prompted to scroll the display. The auto parameter will attempt to determine the screen geometry if provided by the client. If Auto is selected and the client does not supply the value, the default is 24 lines.

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system page-length
```

# Usage 

```
[admin@UplogixLM]# config system page-length
Page length preference is auto.
Change this? (y/n) [n]: y
Page length preference (2 or more lines or auto): 30
```

# History 

3.4 - This command was introduced 

# Related commands 

- **page-length**
- **show system page-length**
