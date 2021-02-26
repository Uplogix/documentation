<!-- 5.4 -->

Local Managers provide basic terminal connections to almost any device with a console port. For certain devices, advanced drivers are available to enable monitoring and management. 

You can view a list of advanced drivers by entering a question mark when prompted for a *Make* in the **config init** command. As of 5.4, this list now includes power controllers.

```
make [native]: ?
'?' is not supported.
Please choose from one of the following values:
 3Com
 Alcatel
 APC
 Avocent
 BayTech
 Brocade
 Cisco
 Comtech
 enhanced
 Foundry
 Garmin
 GE
 Gilat
 HP
 IBM
 iDirect
 Juniper
 Lantronix
 MRV
 native
 ND SatCom
 Netscreen
 Nortel
 PPP
 SeaTel
 server
 ServerTech
 SpaceTrack
 Sun
 Tasman
 Tippingpoint
 TracStar
make [native]: 
```

Since many devices differ in configuration and operation, Configuration Guides have been made available to provide device-specific instructions for managing the device with a Local Manager.

> Some configuration guides make use of the *enhanced native* mode, which provides additional functionality when an advanced driver is not available. 

A general discussion of port initialization is available in the [Initializing Ports](http://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/initializing-ports) topic.

Please refer to the topic listing on the left for a list of currently available configuration guides.