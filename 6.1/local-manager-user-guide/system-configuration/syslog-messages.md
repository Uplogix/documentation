<!-- 5.4 -->

# Overview

This document provides a list of Uplogix Local Manager Syslog messages and their corresponding level for Uplogix version 5.2. 

# Syslog 

Syslog messages can be sourced from the Local Managerâ€™s context as well as from a device port.  Each area can be configured to log to a different server, facility, and UDP port. Uplogix Local Manager specific logs are sourced as the Local Managerâ€™s facility. 

Device logs are collected from the console or buffered log and sent as the device portâ€™s facility.  All Syslog messages are sourced from the Local Managerâ€™s IP address.  

## Local Manager
 
This will include system and port level events including modem, outband, and power components. This is configured with the **config system syslog** command. An example of this type would be: 

```
Jan  31 22:20:36 local3: Host: A500560133 ; NOTICE: User login failed.
Jan  31 22:20:29 local3: Host: A500560133 Duration: 00:15:00 Count: 21; WARNING: Failed to connect to pulse server. (192.0.2.88:7)
Jan  31 22:21:30 local3: Host: hwvpn8; INFORMATIONAL: Port was locked
Jan  31 22:21:30 local3: Host: hwvpn8; WARNING: Terminal is locked. (rbuilder)
```

## Device

Each device port can be configured to send device log messages collected from the deviceâ€™s console port to a specific host. The **config device logging** command from the deviceâ€™s port is used to specify these settings:

```
Jan  31 22:29:20 local4: Host: hwvpn8 189243: *Jan 24 15:37:57.978 UTC: %SEC-6-IPACCESSLOGP: list from_internet denied udp 203.0.113.75(137) (FastEthernet4 50e5.49b8.a010) -> 203.0.113.255(137), 4 packets
Jan  31 22:29:20 local4: Host: hwvpn8 189244: *Jan 24 15:38:57.978 UTC: %SEC-6-IPACCESSLOGP: list from_internet denied udp 203.0.113.75(5353) (FastEthernet4 50e5.49b8.a010) -> 224.0.0.251(5353), 7 packets
Jan  31 22:29:20 local4: Host: hwvpn8 189245: *Jan 24 15:38:57.978 UTC: %SEC-6-IPACCESSLOGP: list from_internet denied udp 203.0.113.75(17500) (FastEthernet4 50e5.49b8.a010) -> 203.0.113.255(17500), 12 packets
```
 
> The current UTC time of the Local Manager is included in each message. The January 31 date is the current time on the Local Manager and the January 24 date (seen later in the message) was included in the text from the device.

# Message Structure

This is a list of available Syslog messages as of Local Manager version 5.2.  All Syslog messages are sent using Universal Coordinated Time (UTC).
 
* Severity Level is sent as a single digit from 0 to 7, indicating the severity of the message.
	* 0 - Emergency
	* 1 - Alert
	* 2 - Critical
	* 3 - Error
	* 4 - Warning
	* 5 - Notice
	* 6 - Info
	* 7 â€“ Debugging
* Equivalent SNMP Event â€“ Each Local Manger Syslog can additionally be sent as an SNMP trap using the MIB definitions listed here.  See the MIB reference for more detail about this.
* Message â€“ This is a text field. The Local Management software or rule authors may append additional information to these messages.

# Uplogix Syslog Protocols


| Level | Equivalent SNMP Event | Message
|- | - | 
| NOTICE | uplogixJobFailed |Scheduled job failed.
| INFO | uplogixDownloadStarted |Download started.
| INFO | uplogixEnvoyBackupStarted |System backup started.
| INFO | uplogixEnvoyRestoreStarted |System restore started.
| INFO | uplogixEnvoyUpdateStarted |System update started.
| INFO | uplogixUploadStarted |Upload started.
| WARNING | uplogixPppUp |PPP is up.
| NOTICE | uplogixPppDown |PPP is down.
| NOTICE | uplogixEnvoyRestart |System restarted.
| NOTICE | uplogixConfigUser |User configured.
| NOTICE | uplogixConfigUserGroup |User group configured.
| NOTICE | uplogixConfigImport |Imported system configuration.
| WARNING | uplogixEnvoyShutdown |System shutdown.
| NOTICE | uplogixEnvoyEnable |Switched user
| NOTICE | uplogixEnvoySuspend |System suspended.
| NOTICE | uplogixEnvoyServiceAccessOn |Service access on
| NOTICE | uplogixEnvoyServiceAccessOff |Service access off
| NOTICE | uplogixFilesystemReadOnly |Appliance filesystem read-only
| WARNING | uplogixVpnUp |VPN is up.
| NOTICE | uplogixVpnDown |VPN is down.
| NOTICE | uplogixEnvoyLogin |User logged in.
| WARNING | uplogixEnvoyCallerDisallowed |Incoming call denied.
| WARNING | uplogixEnvoyPulseFailure |Failed to connect to pulse server.
| NOTICE | uplogixEnvoyPulseRestored |Restored connection to the pulse server.
| WARNING | uplogixEnvoyUSBDisAlarm |USB serial device disconnected from envoy.
| ERROR |uplogixEnvoyUSBNFAlarm |USB serial device not found on system startup.
| NOTICE | uplogixEnvoyLogout |User logged out.
| INFO | uplogixEnvoyNoPowercontrol |No power control configured.
| NOTICE | uplogixEnvoyLoginFailed |User login failed.
| INFO | uplogixEnvoyLoginExceeded |User account locked; too many incorrect logins.
| ERROR |uplogixEnvoyPPPFailed |Unable to establish PPP session.
| NOTICE | uplogixEnvoyTempExceeded |System temperature threshold exceeded.
| WARNING | uplogixEnvoyPowerFailure |Primary power failure
| NOTICE | uplogixEnvoyHumidityExceeded |System humidity threshold exceeded.
| INFO | uplogixEnvoyCallerAllowed |Incoming call allowed.
| NOTICE | uplogixModemLineInUse |Modem line in use.
| NOTICE | uplogixModemLineDisconnected |Modem line disconnected.
| NOTICE | uplogixHeartbeatTimedOut |Heartbeat timed out.
| NOTICE | uplogixHeartbeatFailed |Heartbeat failed.
| NOTICE | uplogixArchiveTimedOut |Archive timed out.
| NOTICE | uplogixArchiveFailed |Archive failed.
| NOTICE | uplogixEnvoyLoginPermissionDenied |User does not have login privilege.
| NOTICE | uplogixEnvoyAndEmsTimeDelta |System and management server clocks are more than 20 seconds out of sync.
| NOTICE | uplogixUnableToResolve |Unable to resolve hostname
| NOTICE | uplogixExportTimedOut |Export timed out.
| NOTICE | uplogixExportFailed |Export failed.
| NOTICE | uplogixNtpServerInvalid |NTP server invalid.
| ERROR |uplogixEnvoyVPNFailed |Unable to establish VPN session.
| NOTICE | uplogixHeartbeatSslFailed |Heartbeat SSL failure.
| NOTICE | uplogixHeartbeatNoClientCertificate |System missing heartbeat client certificate.
| NOTICE | uplogixHeartbeatNoServerCertificate |System missing heartbeat management certificate.
| NOTICE | uplogixHeartbeatFipsMismatch |System and management server have FIPS mode mismatch.
| ERROR |unrecoverableInstallationError |Unrecoverable installation Error
| NOTICE | cpuTempExceeded |CPU temperature threshold exceeded.
| NOTICE | uplogixEnvoyModemConnect |Modem CONNECT.
| NOTICE | uplogixPowerSupplyDown |Power lost.
| NOTICE | uplogixNetworkPrimaryDown |Primary network interface is down.
| NOTICE | uplogixNetworkSecondaryDown |Secondary network interface is down.
| NOTICE | uplogixNetworkTertiaryDown |Tertiary network interface is down.
| WARNING | uplogixCpuLoadMinor |CPU has surpassed a minor threshold.
| ERROR |uplogixCpuLoadMajor |CPU has surpassed a major threshold.
| CRITICAL| uplogixCpuLoadCritical |CPU has surpassed a critical threshold.
| WARNING | uplogixMemoryMinor |Memory has surpassed a minor threshold.
| ERROR |uplogixMemoryMajor |Memory has surpassed a major threshold.
| CRITICAL| uplogixMemoryCritical |Memory has surpassed a critical threshold.
| WARNING | uplogixDiskMinor |Disk has surpassed a minor threshold.
| ERROR |uplogixDiskMajor |Disk has surpassed a major threshold.
| CRITICAL | uplogixDiskCritical |Disk has surpassed a critical threshold.
| NOTICE | uplogixDeviceCyclePower |System is power cycling.
| NOTICE | uplogixOutletOnStarted |Turning on outlet started.
| NOTICE | uplogixPowerCycleStarted |Power cycle started.
| NOTICE | uplogixDeviceReboot |Rebooting device.
| NOTICE | uplogixPowerOffStarted |Power off started.
| NOTICE | uplogixPowerOnStarted |Power on started.
| INFO | uplogixPreparePartitionStarted |Prepare partition started.
| INFO | uplogixPullOSStarted |Pull OS started.
| INFO | uplogixPullRunningConfigStarted |Pull running configuration started.
| INFO | uplogixPullStartupConfigStarted |Pull startup configuration started.
| NOTICE | uplogixPushOSStarted |Push OS started.
| NOTICE | uplogixClearPasswordStarted |Clear password started.
| NOTICE | uplogixPushRollbackConfigStarted |Push rollback configuration started.
| NOTICE | uplogixPushRunningConfigStarted |Push running configuration started.
| NOTICE | uplogixPushStartupConfigStarted |Push startup configuration started.
| WARNING | uplogixRecAttempt |Attempting recovery.
| NOTICE | uplogixRebootStarted |Reboot started.
| INFO | uplogixReceiveFileFtpStarted |Receive file FTP started.
| INFO | uplogixReceiveFileTftpStarted |Receive file TFTP started.
| WARNING | uplogixRecoverConfigurationStarted |Recover configuration started.
| WARNING | uplogixRecoverStarted |Recover started.
| NOTICE | uplogixRommonRemoteBootStarted |Rommon remote boot started.
| NOTICE | uplogixConfigRecoveryStatusStarted |Configuration recovery status started.
| NOTICE | uplogixRommonStatusRecoveryStarted |Rommon status recovery started.
| INFO | uplogixSendFileFtpStarted |Send file FTP started.
| INFO | uplogixSendFileTftpStarted |Send file TFTP started.
| INFO | uplogixSendFileXmodemStarted |Send file Xmodem started.
| NOTICE | uplogixDeviceRecoverySuccessful |Recovery successful.
| INFO | uplogixSetSerialSpeedStarted |Set serial speed started.
| INFO | uplogixShowTechStarted |Show tech started.
| INFO | uplogixSqueezePartitionStarted |Squeeze partition started.
| INFO | uplogixUpdateBootInformationStarted |Update boot information started.
| ERROR |uplogixDeviceRecoveryUnsuccessful |Recovery failed.
| INFO | uplogixDeleteFileStarted |Delete file started.
| INFO | uplogixDeviceLoginFailed |Authentication failure.
| INFO | uplogixAssimilateStarted |Assimilate started.
| NOTICE | uplogixChangeAuthenticationStarted |Change authentication started.
| INFO | uplogixClearCountersStarted |Clear counters started.
| NOTICE | uplogixInterfaceCycleStarted |Interface cycle started.
| NOTICE | uplogixInterfaceOffStarted |Interface off started.
| NOTICE | uplogixInterfaceOnStarted |Interface on started.
| WARNING | uplogixNoStartupConfigRecoveryStarted |No startup configuration recovery started.
| NOTICE | uplogixOutletOffStarted |Turning off outlet started.
| NOTICE | uplogixUserTermedIn |User started a terminal session.
| NOTICE | uplogixUserTermedOut |User completed a terminal session.
| INFO | uplogixCopyFilePortToPort |File copied from one port to another.
| NOTICE | uplogixCopyFileToUrl |File copied to an external location.
| INFO | uplogixCopyFileFromUrl |File copied from an external location.
| NOTICE | uplogixUserTermedOutWithChanges |User completed a terminal session with changes.
| ERROR |uplogixDeviceLogoutFailed |Authentication failure - could not log out.
| INFO | uplogixDeviceIntRely |Reliability is less than 90%.
| INFO | uplogixDeviceIntAborts |Aborted packets exceed threshold.
| INFO | uplogixDeviceIntColl |Output collisions exceed threshold.
| INFO | uplogixDeviceIntDCD |DCD is down.
| INFO | uplogixDeviceIntResets |Resets exceed threshold.
| INFO | uplogixDeviceIntDefferedPkts |Deferred packets exceed threshold.
| INFO | uplogixDeviceIntNoCarrier |No carrier exceed threshold.
| INFO | uplogixDeviceIntCarrierTrans |Carrier transitions exceed threshold.
| INFO | uplogixDeviceIntLOS |Loss of Signal is incrementing.
| INFO | uplogixDeviceIntLOF |Loss of Frame is incrementing.
| INFO | uplogixDeviceIntAIS |AIS Alarm is incrementing.
| INFO | uplogixDeviceIntRunts |Runts exceed threshold.
| INFO | uplogixDeviceIntRemote |Remote Alarm is incrementing.
| INFO | uplogixDeviceIntLineCode |Line Code Violations are incrementing.
| INFO | uplogixDeviceIntPathCode |Path Code Violations are incrementing.
| INFO | uplogixDeviceIntDSR |DSR is down.
| INFO | uplogixDeviceIntFrameLoss |Frame Loss Seconds are incrementing.
| INFO | uplogixDeviceIntLineErrorSeconds |Line Error Seconds are incrementing.
| INFO | uplogixDeviceIntErrorSeconds |Errored Seconds are incrementing.
| INFO | uplogixDeviceIntUnavailableSeconds |Unavailable Seconds are incrementing.
| INFO | uplogixDeviceCyclePowerFailed |Power Cycle failed.
| INFO | uplogixDeviceNoPowercontrol |Device has no power control configured.
| INFO | uplogixDeviceIntGiants |Giants exceed threshold.
| INFO | uplogixDeviceCyclePowerSucceeded |Power Cycle succeeded.
| INFO | uplogixDeviceIntState |Operational state down.
| INFO | uplogixDeviceIntProt |Protocol state down.
| INFO | uplogixDeviceIntLoad |Load is greater than 90%.
| INFO | uplogixDeviceIntDTR |DTR is down.
| INFO | uplogixDeviceIntRTS |RTS is down.
| INFO | uplogixDeviceIntCTS |CTS is down.
| INFO | uplogixDeviceStateDetectFailed |Unable to communicate with device.
| INFO | uplogixDeviceIntOutputQDrops |Output Queue Drops exceed threshold.
| INFO | uplogixDeviceIntInQDrops |Input Queue Drops exceed threshold.
| INFO | uplogixDeviceIntThrottles |Ethernet Throttles exceed threshold.
| INFO | uplogixDeviceIntCRC |CRC Errors exceed threshold.
| INFO | uplogixDeviceIntFrameErr |Frame errors exceed threshold.
| INFO | uplogixDeviceIntOverrunErr |Overrun errors exceed threshold.
| INFO | uplogixDeviceIntLateColl |Late Collisions exceed threshold.
| INFO | uplogixDeviceIntIgnPackets |Ignored Packets exceed threshold.
| NOTICE | uplogixDeviceConsoleDisconnected |Device console port disconnected from envoy.
| INFO | uplogixDeviceSshForwarded |SSH forwarding connection setup to device.
| WARNING | uplogixDeviceVirtualPortError |Virtual-port error.
| NOTICE | uplogixDeviceNearBlockageZone |Device Near a blockage zone.
| NOTICE | uplogixDeviceInBlockageZone |In a blockage zone.
| NOTICE | uplogixDeviceAgcBelowThreshold |AGC is below threshold.
| NOTICE | uplogixDeviceRxUnlocked |RX is unlocked.
| NOTICE | uplogixDeviceTxMuted |TX is muted.
| WARNING | uplogixDeviceOSCurrentNotPolicy |Current OS does not match Policy OS.
| WARNING | terminalLocked |Terminal is locked.
| WARNING | uplogixOsFileNotOnDevice |The device is running a network-booted OS. Please push an OS file to it.
| INFO | uplogixGeneric
| INFO | uplogixGeneric2
| INFO | uplogixGeneric3
| INFO | uplogixGeneric4
| INFO | uplogixGeneric5
| INFO | uplogixGeneric6
| INFO | uplogixGeneric7
| INFO | uplogixGeneric8
| INFO | uplogixGeneric9
| INFO | uplogixGeneric10
| INFO | uplogixGeneric11
| INFO | uplogixGeneric12
| INFO | uplogixGeneric13
| INFO | uplogixGeneric14
| INFO | uplogixGeneric15
| INFO | uplogixGeneric16
| INFO | uplogixGeneric17
| INFO | uplogixGeneric18
| INFO | uplogixGeneric19
| INFO | uplogixGeneric20
| INFO | uplogixGeneric21
| INFO | uplogixGeneric22
| INFO | uplogixGeneric23
| INFO | uplogixGeneric24
| INFO | uplogixGeneric25
| INFO | uplogixGeneric26
| INFO | uplogixGeneric27
| INFO | uplogixGeneric28
| INFO | uplogixGeneric29
| INFO | uplogixGeneric30
| INFO | uplogixGeneric31
| INFO | uplogixGeneric32
| INFO | uplogixGeneric33
| INFO | uplogixGeneric34
| INFO | uplogixGeneric35
| INFO | uplogixGeneric36
| INFO | uplogixGeneric37
| INFO | uplogixGeneric38
| INFO | uplogixGeneric39
| INFO | uplogixGeneric40
| INFO | uplogixGeneric41
| INFO | uplogixGeneric42
| INFO | uplogixGeneric43
| INFO | uplogixGeneric44
| INFO | uplogixGeneric45
| INFO | uplogixGeneric46
| INFO | uplogixGeneric47
| INFO | uplogixGeneric48
| INFO | uplogixGeneric49
| INFO | uplogixGeneric50
| INFO | uplogixDownloadCompleted | Download completed.
| NOTICE | uplogixEnvoyUpdateCompleted |System update completed.
| INFO | uplogixUploadCompleted |Upload completed.
| INFO | uplogixClearedSlot |Slot cleared.
| INFO | uplogixClearedArchiveFiles |Archive files cleared.
| INFO | uplogixClearedExportFiles |Export files cleared.
| INFO | uplogixAssimilateCompleted |Assimilate completed.
| NOTICE | uplogixNoStartupConfigRecoveryCompleted |No startup configuration recovery completed.
| INFO | uplogixPullStartupConfigCompleted |Pull startup configuration completed.
| NOTICE | uplogixChangeAuthenticationCompleted |Change authentication completed.
| NOTICE | uplogixPushOSCompleted |Push OS completed.
| NOTICE | uplogixPushRollbackConfigCompleted |Push rollback configuration completed.
| NOTICE | uplogixPushRunningConfigCompleted |Push running configuration completed.
| NOTICE | uplogixPushStartupConfigCompleted |Push startup configuration completed.
| NOTICE | uplogixRebootCompleted |Reboot completed.
| INFO | uplogixReceiveFileFtpCompleted |Receive file FTP completed.
| INFO | uplogixReceiveFileTftpCompleted |Receive file TFTP completed.
| NOTICE | uplogixRecoverCompleted |Recover completed.
| NOTICE | uplogixOutletOffCompleted |Turning off outlet completed.
| NOTICE | uplogixRecoverConfigurationCompleted |Recover configuration completed.
| NOTICE | uplogixRommonRemoteBootCompleted |Rommon remote boot completed.
| INFO | uplogixClearCountersCompleted |Clear counters completed.
| NOTICE | uplogixRommonStatusRecoveryCompleted |Rommon status recovery completed.
| INFO | uplogixSendFileFtpCompleted |Send file FTP completed.
| INFO | uplogixSendFileTftpCompleted |Send file TFTP completed.
| INFO | uplogixSendFileXmodemCompleted |Send file Xmodem completed.
| INFO | uplogixSetSerialSpeedCompleted |Set serial speed completed.
| INFO | uplogixShowTechCompleted |Show tech completed.
| INFO | uplogixSqueezePartitionCompleted |Squeeze partition completed.
| NOTICE | uplogixOutletOnCompleted |Turning on outlet completed.
| INFO | uplogixUpdateBootInformationCompleted |Update boot information completed.
| INFO | uplogixClearPasswordCompleted |Clear password completed.
| NOTICE | uplogixConfigRecoveryStatusCompleted |Configuration recovery status completed.
| INFO | uplogixDeleteFileCompleted |Delete file completed.
| NOTICE | uplogixInterfaceCycleCompleted |Interface cycle completed.
| NOTICE | uplogixInterfaceOffCompleted |Interface off completed.
| NOTICE | uplogixInterfaceOnCompleted |Interface on completed.
| NOTICE | uplogixPowerCycleCompleted |Power cycle completed.
| NOTICE | uplogixPowerOffCompleted |Power off completed.
| NOTICE | uplogixPowerOnCompleted |Power on completed.
| INFO | uplogixPreparePartitionCompleted |Prepare partition completed.
| INFO | uplogixPullOSCompleted |Pull OS completed.
| INFO | uplogixPullRunningConfigCompleted |Pull running configuration completed.
| INFO | uplogixClearedPort |Port cleared.
| INFO | uplogixPppCycleDurationCompleted |PPP cycle duration completed.
| INFO | uplogixPppCycleHeartbeatCompleted |PPP cycle heartbeat completed.
| WARNING | uplogixAssimilateFailed |Assimilate failed.
| WARNING | uplogixNoStartupConfigRecoveryFailed |No startup configuration recovery failed.
| WARNING | uplogixPullStartupConfigFailed |Pull startup configuration failed.
| WARNING | uplogixChangeAuthenticationFailed |Change authentication failed.
| WARNING | uplogixPushOSFailed |Push OS failed.
| WARNING | uplogixPushRollbackConfigFailed |Push rollback configuration failed.
| WARNING | uplogixPushRunningConfigFailed |Push running configuration failed.
| WARNING | uplogixPushStartupConfigFailed |Push startup configuration failed.
| WARNING | uplogixRebootFailed |Reboot failed.
| WARNING | uplogixReceiveFileFtpFailed |Receive file FTP failed.
| WARNING | uplogixReceiveFileTftpFailed |Receive file TFTP failed.
| WARNING | uplogixRecoverFailed |Recover failed.
| WARNING | uplogixOutletOffFailed |Turning off outlet failed.
| WARNING | uplogixRecoverConfigurationFailed |Recover configuration failed.
| WARNING | uplogixRommonRemoteBootFailed |Rommon remote boot failed.
| WARNING | uplogixClearCountersFailed |Clear counters failed.
| WARNING | uplogixRommonStatusRecoveryFailed |Rommon status recovery failed.
| WARNING | uplogixSendFileFtpFailed |Send file FTP failed.
| WARNING | uplogixSendFileTftpFailed |Send file TFTP failed.
| WARNING | uplogixSendFileXmodemFailed |Send file Xmodem failed.
| WARNING | uplogixSetSerialSpeedFailed |Set serial speed failed.
| WARNING | uplogixShowTechFailed |Show tech failed.
| WARNING | uplogixSqueezePartitionFailed |Squeeze partition failed.
| WARNING | uplogixOutletOnFailed |Turning on outlet failed.
| WARNING | uplogixUpdateBootInformationFailed |Update boot information failed.
| WARNING | uplogixClearPasswordFailed |Clear password failed.
| WARNING | uplogixConfigRecoveryStatusFailed |Configuration recovery status failed.
| WARNING | uplogixDeleteFileFailed |Delete file failed.
| WARNING | uplogixInterfaceCycleFailed |Interface cycle failed.
| WARNING | uplogixInterfaceOffFailed |Interface off failed.
| WARNING | uplogixInterfaceOnFailed |Interface on failed.
| WARNING | uplogixPowerCycleFailed |Power cycle failed.
| WARNING | uplogixPowerOffFailed |Power off failed.
| WARNING | uplogixPowerOnFailed |Power on failed.
| WARNING | uplogixPreparePartitionFailed |Prepare partition failed.
| WARNING | uplogixPullOSFailed |Pull OS failed.
| WARNING | uplogixPullRunningConfigFailed |Pull running configuration failed.
| WARNING | uplogixDownloadFailed |Download failed.
| WARNING | uplogixEnvoyBackupFailed |System backup failed.
| WARNING | uplogixEnvoyRestoreFailed |System restore failed.
| WARNING | uplogixEnvoyUpdateFailed |System update failed.
| WARNING | uplogixUploadFailed |Upload failed.
| WARNING | uplogixIptTestFailed |SLV test failed.
| WARNING | uplogixScheduleJobFailed |Failed to schedule job.
| WARNING | uplogixPppCycleDurationFailed |PPP cycle duration failed.
| WARNING | uplogixPppCycleHeartbeatFailed |PPP cycle heartbeat failed.
| WARNING | uplogixCollectGpsFailed |Collect GPS failed.
| WARNING | uplogixSetPositionFailed |Set GPS position failed.
| WARNING | uplogixCollectRemoteStateStatsFailed |Collect remote state stats failed.
| WARNING | uplogixModemCheckFailed |Modem Check Failed
| ERROR |uplogixFilesystemLow |Appliance filesystem out of space
| ERROR |uplogixVpdInaccessible |Appliance VPD inaccessible
| ERROR |ethernetInterfaceTurnedOff |Ethernet interface turned off