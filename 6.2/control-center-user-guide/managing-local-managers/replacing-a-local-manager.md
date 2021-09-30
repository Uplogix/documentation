<!-- 5.4 -->
<div class='ucc' />Inventory > Local Manager Summary</div>
# Overview

If a Local Manager encounters an unrecoverable hardware or software error, it will likely need to be replaced with a new unit. To make the transition smoother, the Control Center can automatically copy data from the old unit to the new one.

To use this feature, click the *Replace* button on the Local Manager Summary page.

The *Replace* button will be disabled if the Local Manager is heartbeating. The Local Manager needs to have stopped heartbeating for the last four intervals (two minutes at the default thirty-second interval). 

> The Replace function should not be used on systems experiencing temporary heartbeat issues. 

![Uplogix Control Center - Local Manager Summary Page](http://uplogix.com/support/docs/img/6.0/uplogix-control-center-local-manager-summary-replace.png)

Click **Replace** for a list of Local Managers that are available to replace the unresponsive Local Manager. To be listed, a Local Manager must be unassigned, running the same software version as the Control Center, and communicating properly. 

Select a replacement. The unresponsive Local Manager is replaced in the inventory list by the Local Manager selected. The Control Center pushes the stored network device configuration from the replaced Local Manager to the replacement.

After the replacement Local Manager is updated, disconnect all devices from the replaced unit and connect them to the corresponding connectors on the replacement.

# Requirements

Due to differences in configuration data and schema, the following requirements must be met to replace a Local Manager:

* Identical Product - A Local Manager can only be replaced by a Local Manager of the same model. For example, an Uplogix 5000 for an Uplogix 5000. An Uplogix 500 cannot replace a 5000.
* Similar Software Versions - The same **minor** version of software must be on the Local Manager and the UCC. For example, you can replace a 5.3.1 with a 5.3.4, but not with a 5.2.1.
