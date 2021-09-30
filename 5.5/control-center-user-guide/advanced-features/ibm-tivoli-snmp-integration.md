<!-- 5.4 -->

This guide contains instructions for configuring an Uplogix Control Center to send SNMP traps to a Tivoli Netcool instance. Instructions for installing and customizing a rules file in Tivoli follow.

# Requirements
* Uplogix Control Center on version 3.5 or higher
* Tivoli Netcool version 7.3.1
* Mttrapd SNMP probe installed on Tivoli Netcool instance

# Configuring the Uplogix Control Center

<div class='ucc' />Administration > Server Settings > SNMP</div>

To configure the Uplogix Control Center to send SNMP traps to a Tivoli Netcool instance, navigate to the Administration tab in your Control Center's GUI. Under Server Settings, open the SNMP Settings section. Click the Use SNMP check box, enter the IP address or hostname of your Tivoli Netcool instance in the Primary Host Name section. If your Tivoli Netcool instance is configured to listen for traps on a port other then 162, change the port from the default of 162. Finally, enter the read community you would like to use for the SNMP traps.

![Uplogix Control Center SNMP Settings](http://uplogix.com/support/docs/img/5.4/uplogix_control_center_snmp_settings.jpg)

The Uplogix Control Center can be configured to send SNMP traps to up to two SNMP receivers. Configuring either the primary or secondary for Tivoli Netcool is acceptable.

# Installing MTTRAPD Rules File on Tivoli Netcool

To install the MTTRAPD rules file for on your Tivoli Netcool instance, copy the provided mttrapd.rules file into the /opt/IBM/tivoli/netcool/omnibus/probes/linux2x86/ directory. Alternatively the contents of that file can be appended into the existing mttrapd.rules file. After copying or appending the file, restart the mttrapd process.

# Customizing the MTTRAPD Rules File on Tivoli Netcool

To change the severity of incoming traps in Tivoli Netcool, edit the mttrapd.rules file and change the each trap's Severity field to the severity level appropriate to the event's importance (see table one below as an example).

![Uplogix Control Center SNMP Settings](http://uplogix.com/support/docs/img/5.4/uplogix_control_center_snmp_settings_mib.jpg)

Table 1: Netcool/OMNIbus Severity Levels

| Severity | Description | Desktop Color
|---|---|---|
|5 | Critical | Red
|4 |Major	|Orange
|3 |	Minor|	Yellow
|2	|Informational	|Blue
|1	|Indeterminate	|Purple
|0	|Clear	|Green

# Sample mttrapd.rules

Download a sample file [here](http://uplogix.com/docs/pdf/misc/mttrapd.rules).