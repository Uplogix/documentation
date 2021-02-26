# Overview

This document contains best practices, tips, and tricks for the Uplogix product family.

# User Management

* If you have more than 20 users, consider offloading Authentication to TACACS or RADIUS
* Create groups and add users to groups (may be multiple groups per user)
* Add email address to user account for alerting and reporting
* Disable users instead of deleting
* Use lowercase for all usernames unless required by TACACS/RADIUS; usernames are case-sensitive

# Security

* Disable the â€œadminâ€ user
* Disable the â€œadministratorâ€ user
* Assign privileges to groups, not to individual users
* Keep the default â€œdeny use system authâ€ permission to ensure users authenticate with managed devices.
* When creating roles, subtract permissions from the default â€œadminâ€ role instead of building a new role from scratch
* If using third-party AAA:
	* Cache passwords
	* Enable failover to local passwords when the network is down
* If forwarding Auditing information, use *stop-only.*

# Control Center Configuration

* Change emsadminâ€™s password
	* Changing the root password is NOT recommended. It cannot be recovered if it is lost / forgotten. (The root user is not allowed to log in via SSH.)
* Configure NTP
* Enable echo service

# Local Manager Configuration

* Connect both power supplies
* Connect both Ethernet ports (GE-0/GE-1) if using bonded mode

# Out-of-Band

* Schedule a **ppp cycle** job to continually test the out-of-band connection
* Schedule a dialtone test for v92 modems

# Device Management

* Verify serial communication using the *terminal* command prior to initializing port
* Ensure IOS and ROMMON baud rates are the same
* Create a functional account for Local Managers to use when managing devices
* Make use of advanced drivers where possible
* Enable all passive monitoring
* Allow LM to clear device log on managed device

# Reports

* Subscribe to the â€œno heartbeatâ€ report to stay informed of LMs that have gone offline
* Subscribe to the â€œFailed Loginsâ€ report; this will show you if someone is trying to break into your Local Managers