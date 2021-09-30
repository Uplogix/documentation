<!-- 5.4 -->

# Overview

If you are experiencing an issue with your Uplogix Local Manager and you suspect it could be hardware related, please contact us immediately so we can determine if the appliance will need to be returned.

* Phone: 512-857-7070
* Phone: 888-663-6869 (toll-free)
* Email: support@uplogix.com
* URL: [support.uplogix.com/hc/en-us/requests/new](https://support.uplogix.com/hc/en-us/requests/new)

# Troubleshooting

When you contact us for a suspected hardware problem, we'll first attempt to troubleshoot the issue remotely. Some troubleshooting can be done through email; other issues are better resolved over the phone, or even via a remote desktop session.

If an RMA is determined to be necessary, we will request the following:

* Serial Number:
* Description of Problem:
* Shipping Address:
* Contact Name:
* Contact Phone Number:
* Contact Email Address:
* Requested Software Version:

> The software version is needed so we can load your replacement with the appropriate code.

Once we have this information we'll send your replacement and follow up with a tracking number as it becomes available.

Before we process an RMA, we must check on the Local Manager's maintenance contract using the Serial Number. A typical maintenance contract lasts 1 year. In the event that your maintenance contract has expired, we will inform your sales representative to find a solution.

# Building the Replacement

Once the RMA paperwork is complete, the ticket is handed over to Operations to build, provision, and ship the replacement. The requested version of code will be loaded onto the Local Manager prior to shipping.

RMAs must be submitted, processed, and built prior to 4pm Central to ship the same day. RMAs that do not make the cutoff will be shipped the next business day.

Replacements will ship to the country on the original shipping order.

<div class='warning' /><i class='fa fa-globe'></i> International shipments may be subject to local duties and taxes upon arrival. Per your maintenance agreement, these duties and taxes are the responsibility of the customer. You may be able to recover this cost, however, Uplogix is unable to do so on your behalf.</div>

# Returning the Defective Unit

To return the defective unit, use the return labels included with your replacement's 
package.

For international RMAs, return labels will often be sent via email to the contact email address provided.

Use the replacement's packaging to return the defective unit.

**The defective unit is due within 30 days of reception of the replacement**. However, exceptions can be made for Local Managers that are in remote locations such as ships, oil rigs, or other destinations that cannot be easily accessed.

Reminders will be sent if the unit is more than 30 or 60 days overdue. **After 90 days, an invoice will be sent for the replacement unit.**

Upon receiving the defective unit, we will confirm its receipt and close the case within a few days.

# Replacing a Local Manager

When you receive your replacement you may need to make a few changes to it before powering it up and connecting it to your network.

## Replacing a u5000

Make sure your defective unit and replacement Local Manager are powered off and unplugged from any power source.

* Remove the option cards from the defective unit using the thumbscrews.
* Install the option cards in the replacement Local Manager.
* Remove the two screws securing the modem port.
* Install the modem on the replacement Local Manager.

You may now plug in your u5000 and configure its network settings with either the Front Panel LCD or the CLI via the console port.

If you are using a Control Center, enable management of the u5000 with the **config system management** command.

On the Control Center, use the Replace button on the previous Local Manager before assigning the replacement into an Inventory group.



## Replacing a u500

First, make sure your original and replacement Local Managers are powered off and unplugged from any power source.

Remove the two screws securing the modem port.

Install the modem on the replacement Local Manager. First, make sure to plug in the modem. Next, screw in the screws and replace the faceplate.

You may now plug in your u500 and configure its network settings from the CLI using the console cable. If you are using a Control Center, go ahead and point the u500 at it now, using the **config system management** command from the CLI.

On the Control Center, use the Replace button on the previous Local Manager before assigning the replacement into an Inventory group.

# Using the REPLACE button

Log into the Control Center's web app and select the "Inventory Tab" at the upper left hand corner of the screen. The new Local Manager's serial number will appear under the "Unassigned" group after a couple of heartbeats.

Select the old Local Manager and click the Replace button in the upper left hand side of the screen.

Select the replacement Local Manager and click Save.