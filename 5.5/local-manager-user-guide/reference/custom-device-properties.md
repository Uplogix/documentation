<!-- 5.4 -->

The following custom device properties are available for configuration on the Local Managers.

| Property | Description |
| :-- | :-- |
| sysContact.0 | When SNMP is enabled on the Local Manager, defines the system contact. |
| sysLocation.0 | When SNMP is enabled on the Local Manager, defines the system location. Useful if the Local Manager is behind a firewall or NAT.
| sshPort | This property overrides the default port 22 for SSH connections. Useful if the Local Manger is behind a router with port forwarding capabilities.
| sshIp | This property overrides the reported IP address when initiating an SSH connection with the CLI applet.
| sshIpv6 | Specifies an alternate IPv6 address to be used instead of the address reported by the Local Manager.
| sshPortOob | This property overrides the default port 22 for SSH connections while the Local Manager is operating out-of-band.
| sshIpOob | This property overrides the reported out-of-band IP address. Useful if the Local Manager is behind a firewall or NAT when it brings up its out of band connection.
| sshIpv6Oob | Specifies an alternate IPv6 addressed to be used when the Local Manager is operating out-of-band.
| _csr_OU | For use when placing the Local Manager in FIPS mode, the property defines the Organization Unit required when generating a certificate.
| _csr_CN | For use when placing the Local Manager in FIPS mode, the property defines the Common Name required when generating a certificate.
| _csr_O | For use when placing the Local Manager in FIPS mode, the property defines the Organization required when generating a certificate.
| _csr_L | For use when placing the Local Manager in FIPS mode, the property defines the Location required when generating a certificate.
| _csr_ST | For use when placing the Local Manager in FIPS mode, the property defines the State required when generating a certificate.
| _csr_C	 | For use when placing the Local Manager in FIPS mode, the property defines the Country required when generating a certificate.
| _csr_E	| For use when placing the Local Manager in FIPS mode, the property defines the Email Address required when generating a certificate.
| _csr_other | For use when placing the Local Manager in FIPS mode, the property defines other elements that the user may wish to include when generating a certificate.
| forwardIpAddress | Set IP address for forwarding inbound UDP packets.
| readCommunity | Configuration information specific to ND SatCom.
| writeCommunity | Configuration information specific to ND SatCom.
| Enhanced_CommandPrompt | Define an enhanced driver's command prompt.
| Enhanced_PasswordPrompt | Define an enhanced driver's password prompt.
| Enhanced_LoginPrompt | Define an enhanced driver's login prompt.
| Enhanced_LogoutCommand | Define an enhanced driver's logout command.
| Enhanced_TimeoutSeconds | Define an enhanced driver's timeout duration in seconds.
| Enhanced_WakeupCommand | Define an enhanced driver's command to wake up a managed device.
| safedelay | Define a delay period for use after a command is run.
| safeDebug | For use on Sea Tel devices, define for extra log messages on the console during Push OS.
| _powerOnValidationTimeout | Defines a time in milliseconds for the system to wait before checking CTS and DSR during a power on or power cycle operation.
| debug | For RFC-2217 "TCP" connections and/or virtual ports set property for extra log messages on the console.
| _keepalive | For use with virtual ports on Cisco devices, configure a message or character to be sent to maintain the connection.
| _ROMMON_* | During a ROMmon recovery, ROMmon variables defined in this property will be passed to the Cisco device.
| remoteHostOrIpAddress | For use when connecting to an IP address or port via the management Ethernet on the Local Manager, this property defines that destination host or IP Address.
| tcpPort | For use when connecting to an IP address or port via the management Ethernet on the Local Manager, this property defines that destination port.
| _applet_failover_ssh_ip	 | Set the failover SSH IP address when configuring the CLI applet to failover directly to a managed device.
| _applet_failover_ssh_port | Set the failover SSH port when configuring the CLI applet to failover directly to a managed device.
| _applet_failover_ssh_fingerprint | Set the SSH fingerprint when configuring the CLI applet to failover directly to a managed device.
| _lcp_echo_interval | Define the value in seconds between LCP echo requests. Set property to 0 to disable LCP echo.
| _lcp_echo_failure | Define the number of subsequent failures before a PPP link goes down.
| _modem_monitor_init | This property overrides the modem initialization string on the modem monitor.
| _modem_monitor_test | This property provides a test dial string on the modem monitor.
| \_snmp\_1.3.6.1.4.1.10243.10.1.5.5 | Set to "enable" if customer has a GPS attached to their Local Manager and would like the statistics to show up in SNMP.
| \_snmp\_.1.3.6.1.4.1.2021.10.1 | Set to "enable" to get SNMP Load Average (UCD-SNMP-MIB).
| \_snmp\_.1.3.6.1.2.1.25.2.3.1.1.1 | Set to "enable" to get SNMP Memory Info (HOST-RESOURCES-MIB).
| \_snmp\_.1.3.6.1.2.1.25.2.3.1.1.31 | Set to "enable" to get SNMP Disk Info (HOST-RESOURCES-MIB).