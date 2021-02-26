<!-- 5.4 -->
<div class='ucc' />Inventory</div>

# Overview

To view an expandable tree view of inventory, select the Inventory tab.

![Uplogix Control Center Inventory](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-inventory.png)
 
The current organization of your deployment is shown, including inventory groups and individual Local Managers. Initially, the Inventory list shows only the two default groups, *Your Company* and *Unassigned*. Additional groups will be sorted alphabetically. 

To search for a specific Local Manager, use the Search box in the Navigation bar and enter a hostname or serial number.

To view the contents of an inventory group, click the expand icon to the left of the inventory group name. To view the group details, click the group name and the group detail page displays. All functions concerning inventory groups can be accessed from the group detail page.

A gray icon indicates the group is empty.

The icons beside each entry denote status or other information.

# Quick Status

|Icon |Description|
|:--|:---|
|![](http://uplogix.com/support/docs/img/cc-user-guide/image017.png)| 	Inventory group is collapsed.<br>â€¢	Black arrow indicates the group contains at least one Local Manager or child group.<br>â€¢	Gray indicates the group is empty.|
|![](http://uplogix.com/support/docs/img/cc-user-guide/image018.png)| 	Inventory group is expanded, listing the Local Managers and child groups.|
|![](http://uplogix.com/support/docs/img/cc-user-guide/image019.png)| 	The Local Manager has communicated within the past four heartbeat intervals. The default interval is 30 seconds.|
|![](http://uplogix.com/support/docs/img/cc-user-guide/image020.png)| 	No communication has been received from this Local Manager within the past four heartbeat intervals.|
|![](http://uplogix.com/support/docs/img/cc-user-guide/image021.png)| 	This unit is communicating in minimal heartbeat mode. Commonly indicating local managers using an older version of Local Manager software. |
|![](http://uplogix.com/support/docs/img/cc-user-guide/image022.png)| 	This unit is communicating over the Outband (out-of-band) connection.|
|![](http://uplogix.com/support/docs/img/cc-user-guide/image023.png)| 	The unit has been manually added (pre-provisioned) to the inventory, but has not yet contacted the server.|

# Other information

## SSH button

Launches the Control Center's SSH applet, which is a Java application that runs locally on the user's workstation.

## Status

Displays either a green checkmark to indicate "good" status or a red icon to indicate alarms are present.

## CON / ETH

These icons are green when the Local Manager detects a connection on its console and ethernet ports.

## IP

The IP address of the Local Manager (as reported by the LM)

## Uptime

How long the Local Manager has been running

## Last Alarm

Time since the last alarm was generated on the Local Manager.

## Last Event

Time since the last event was logged on the Local Manager.