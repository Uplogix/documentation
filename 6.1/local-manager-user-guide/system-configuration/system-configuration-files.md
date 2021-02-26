Use this feature to back up Local Manager configuration data to an external source.

The **config export** command uses FTP, SCP, or USB to export the Local Manager configuration as an XML file to a specified location. The XML file can be loaded back onto the Local Manager using the **config import** command. Use the **show config** command to view the data that will be exported.

```
[admin@UplogixLM]# config export ?
usage: export <method> <target>
methods: ftp, scp, usb

Export via FTP or SCP
ex. config export ftp <userId@host:fileName>
ex. config export scp <userId@host:fileName>
Export via USB
ex. config export usb <fileName>
```

Here's an example of a successfull and failed configuration export.

```
[admin@UplogixLM]# config export scp admin@172.30.4.225:UplogixLM.xml
Password: *******
File successfully sent to 172.30.4.225.

[admin@UplogixLM]# config export scp admin@172.30.4.227:UplogixLM.xml
Password: *******
Failed to send '/storage/tmp/exportedConfig.xml' to '172.30.4.227' via scp.
```

To import a configuration file, use the **config import** command:

```
[admin@UplogixLM]# config import scp admin@172.30.4.227:Uplogix.xml
password: *******
160,771 bytes read (100%) done
Retrieved 'Uplogix.xml' from 172.30.4.227.
Removing users and groups from import xml.
Removing permissions from import xml.
Removing admin role from import xml; it is not editable.
Database closed
Currently cannot import option cards; ignoring them.
Importing virtual ports.
```

An XML file should only be loaded onto a Local Manager running the same software version or a higher software version as the Local Manager from which the file was exported.

```
[admin@UplogixLM]# show config
<?xml version="1.0" encoding="UTF-8"?>
<EnvoyConfiguration>
    <version>6.0</version>
    <roles>
        <role>
            <name>admin</name>
            <permissions>
                <permission>
                    <name>allow assimilate</name>
                </permission>
                <permission>
                    <name>allow autorecovery</name>
                </permission>
                <permission>
                    <name>allow capture</name>
                </permission>
                <permission>
                    <name>allow certify</name>
                </permission>
                <permission>
                    <name>allow clear counters</name>
                </permission>
                <permission>
                    <name>allow clear log</name>
                </permission>
                <permission>
                    <name>allow clear password</name>
                </permission>
                <permission>
                    <name>allow clear service-module</name>
                </permission>
                <permission>
                    <name>allow clear xbrowser</name>
                </permission>
                <permission>
                    <name>allow config aaa</name>
                </permission>
```