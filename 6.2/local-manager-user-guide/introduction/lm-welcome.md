# Overview
The **Local Manager User Guide** describes the configuration, management, and advanced features of the Uplogix Local Manager. The information presented applies to all models of the Local Manager except where otherwise noted.

# Typographical Conventions

The following conventions are used in this guide.

Sample text from the Uplogix command line interface is presented as preformatted text. For example:

```
[admin@UplogixLM]# show who
admin ssh Mar 22 13:38 (203.0.113.6)
```

Keyboard characters are enclosed in square brackets. For example, press [Enter].

Navigation paths to command equivalents on a Control Center are shown in italics. For example:

<div class='ucc' />Administration > Server Settings</div>

# Safety Summary

Following all cautions and warnings will ensure your own safety and protect the Local Manager from potential damage or loss of data.

<div class='warning' />Read all installation instructions before connecting the Local Manager to a power source.</div>

Read and understand the following instructions before using the Local Manager:

* Use three wire electrical extension cords with a current rating equal to or greater than the Local Manager's current rating.
* Always disconnect the Local Manager from power before cleaning and servicing.
* Do not spray liquids directly onto the Local Manager when cleaning. Always apply the liquid first to a static free cloth.
* Do not immerse the Local Manager in any liquid or place any liquids on it.
* Do not disassemble the Local Manager. Hazardous voltages are present inside the Uplogix 5000 system and can result in injury or death. To reduce the risk of shock and to maintain the warranty on the device, a qualified technician must perform service or repair work.
* Connect the Local Manager to a grounded outlet. 
* Only connect the Local Manager to surge-protected power outlets.

# Uplogix Glossary

| Term | Definition |
| :--- | :--- |
| **Archive** | Local Managers send bulk data, such as: session logs, change logs, and all other non-urgent statistical data to the Control Center every 60 minutes (default) using an encrypted HTTPS proprietary data communication protocol on port 8443. |
| **Heartbeat** | Local Managers communicate with the Control Center every 30 seconds (default) using a secure HTTPS proprietary communication protocol on TCP port 8443. Device state, alarms, events and configuration parameters are sent during a heartbeat. |
| **Local Manager (LM)** | An Uplogix local management appliance that is directly connected to managed network devices and servers. |
| **Pulse** | Used by the Local Manager to determine network connectivity by sending data to an echo server on TCP port 7 (echo) every 30 seconds. Up to three may be defined to determine failure. **Learn More:** [Using the Pulse Feature](http://uplogix.com/docs/local-manager-user-guide/out-of-band-configuration/using-the-pulse-feature) |
| **Uplogix LM80** | The Uplogix LM80 Local Manager is a compact, fixed 8-port model that can be used to manage 8 devices. |
| **Uplogix LM83X**| The Uplogix LM83X Local Manager is a modular chassis model with higher port density that can scale to manage 56 directly connected devices. |
| **Uplogix 500** | The Uplogix 500 Local Manager appliance is a compact, fixed 6-port model that can be used to manage 6 devices. |
| **Uplogix 5000** | The Uplogix 5000 Local Manager appliance is a modular chassis model with higher port density that can scale to manage 38 directly connected devices. |
| **Uplogix Control Center (UCC)** | Centralized element manager for all Local Managers and their managed devices deployed throughout the network. The web-based graphical user interface (GUI) enables IT administrators to easily view, manage, configure and control all network devices and servers connected to Local Managers and supplies access to real time data from these devices. The Control Center is also the integration point for all remotely collected data and diagnostics for upstream delivery to NMS tools such as Solarwinds, HP OpenView, CA Spectrum, and Tivoli Netcool. |