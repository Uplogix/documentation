<!-- 5.4 -->

# Overview

The topics in this section describe the configuration of managed devices and related power settings. To provide useful examples, most topics focus on the configuration and management of a **Cisco router**. 

For instructions specific to your device, see [Configuration Guides](http://uplogix.com/docs/local-manager-user-guide/configuration-guides).

The initial configuration of a port resource must be done from the Local Manager's CLI. Some management features are available from the Uplogix Control Center once the port has been configured.

# Native Mode

By default, ports on the Local Manager are configured as *native*. This mode provides basic console access to a managed device. Use this mode to test connectivity between the Local Manager and the managed device or in situations where no Enhanced or Advanced driver exists for your make/model.

A device configured as native can be controlled by a serial connection and by the power control unit, but can only monitor chassis statistics gathered externally such as Ethernet link beat and serial CTS/DSR/TX/RX.