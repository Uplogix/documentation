# Description

The Uplogix Local Manager sends bulk data such as session logs, change logs, device files, and all other non-urgent statistical data to the Control Center at regular intervals (60 minutes by default). This alarm is an indication that this data (archive) has failed to reach the Control Center at its scheduled interval.

# Steps to Resolve

The steps to clear the alarm involve determining the point of failure from the Local Manager to the Control Center.

## Is a firewall blocking the archive?

Archiving occurs over port 8443, so verify that if you have a firewall on your network, it's allowing transmission through port 8443.

## Are the Local Manager and Control Center running the same version of software?

Archive requires the Local Manager to be fully heartbeating with the Control Center. If there is a software version mismatch between the LM and the UCC, it will operate in minimal heartbeat mode and archive is suspended. Verify that your appliance(s) are running the same software version as your UCC.

## Is the Local Manager running in out-of-band mode?

By default, archiving is suspended when the LM is operating in out-of-band mode due to limited bandwidth of dial-up connections. Once in-band connectivity is restored, archive will also be restored. You can configure archive to operate over the out-of-band connection by running the **config system archive** from the system resource.

If you are still seeing this alarm after verifying all the above, run the command **config system clear archive** from the system resource to see if it clears the alarm.

Please contact Uplogix Support if you are unable to clear the alarm after following the above steps.