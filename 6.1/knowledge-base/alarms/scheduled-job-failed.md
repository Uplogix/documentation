#Description

<a href="http://uplogix.com/docs/local-manager-user-guide/configuring-managed-devices/scheduling-jobs-and-monitors">Jobs</a> are discrete tasks that the Local Manager uses to collect information about the device it is managing. This alarm is an indication that a job has failed to due to the Local Manager having an issue communicating with the managed device.  


#Steps to Resolve

The steps to clear the alarm involve determining the point failure from the Local Manager and the Managed device. 



## Is the Local Manager able to successfully login to the device?

If you are seeing this alarm in conjunction with an "authentication failure" alarm, the scheduled job has failed because the Local Manager is having an issue logging into the device. Please see the <a href="http://uplogix.com/docs/alarms/device-management">Authentication failure</a> alarm page to take the necessary steps to correctly configure authentication.

## Is the cabling from the Local Manager to the device working?

Check the physical connection and make sure that the cable connecting the two is working as intended. Replace with a known working cable if possible.


