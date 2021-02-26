<!-- 5.4 -->

Opens an editor that allows you to filter management IP connectivity to the Uplogix Local Manager. Using source IP address as a parameter, the system specifically allows or denies listed IP address/subnet mask combinations. 

# Command availability 

CLI resource: system

Uplogix system: All

LMS offerings: All

# Syntax 

```
config system protocols filter
```

# Subcommands 

**[no] allow [â€œip|ipv6 address/subnet maskâ€]**

**[no] deny [â€œip|ipv6 address/subnet maskâ€]**

**show**

**exit**

#Usage 

The initial filter is **allow all**.

Once filtering is implemented, all managed device IP addresses must be specified in config info for each port to allow TFTP/FTP traffic to the system.

Subnet mask bits can be entered in either decimal (/27) or dotted-decimal (255.255.255.252).

Changes affect new connections to the system. Changes are applied when you exit the editor.

Improper subnet boundaries will be corrected automatically to the closest complete range.

Specifically denied addresses are filtered from those specifically allowed. The **all** keyword is overridden by any specific **allow** or **deny** statement. If you issue the **deny all** command after allowing an address, that address remains allowed. In the example below, all addresses that have not been explicitly allowed will be denied. 

```
[admin@UplogixLM]# config system protocols filter
[config system protocols filter]# allow 172.16.100.80/28
[config system protocols filter]# allow 2001:DB8:1e0:30::0/32
[config system protocols filter]# deny all
[config system protocols filter]# exit
[admin@UplogixLM]#
```

# In the Uplogix web interface

**Inventory > group page > Network > Protocols > IP Filtering** - specific to this inventory group

**Inventory > Local Manager page > Network > Protocols > IP Filtering** - specific to this system

# History 

3.4 - This command was introduced

4.3 â€“ Added IPv6 filters

# Related commands 

- **show system protocols**
