# Description

This alarm is to notify you that the clock on the Local Manager and Control Center are not synchronized. Because Local Managers have many features that depend on timing, it is important that they remain in sync to ensure accurate reporting.

# Steps to Resolve

For the times to be in sync, the Local Manager and the UCC either need to be pointed at the same NTP server, or their times need to be configured manually. Control Centers should arrive with their clocks already synchronized to UTC time. Verify that you currently have NTP configured correctly on the appliances and Control Center.

If your appliance(s) will be managed by the UCC you must update the NTP info on the UCC. You can update this on a group or appliance level by clicking the 'NTP' link on the left side of the appliance/group screen.

![NTP Settings on UCC](http://uplogix.com/support/docs/img/UCC-NTP-03.jpg)

If you are using a hostname for the NTP server (instead of an IP address), DNS must be configured. This can also be done on a group or appliance level by clicking the 'DNS' link on the left side of the appliance/group screen.

Please see <a href="http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/ntp-settings">NTP Settings</a> for steps to configure NTP Settings on the UCC via the CLI.

Please see <a href="http://uplogix.com/docs/local-manager-user-guide/system-configuration/date-and-time">Date and Time </a> to set the date and time manually on a Local Manager.