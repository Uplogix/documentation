<!-- 5.5.4 -->

By default, only Secure Shell version 2 connections are allowed to communicate with the Local Manager. File servers using TFTP, FTP, and SFTP are available for serving files to network devices, but only within specific file transfer operations such as push OS, and in many cases that communication is directly limited to a specific IP address or dedicated network connection.

# SSH Version 2

Secure Shell version 2 is the default user method of communicating with the Local Manager. Users may authenticate using passwords, certificates, or a combination of both. Local Managers recognize both DSA and RSA encryption methods with key length up to 2048 bytes. Encryption is configurable. The default secure shell port (TCP 22) may be changed to any port between TCP 1024 and 65000.

Client SSH applications can be used to access the Local Manager directly. Supported clients include:

- PuTTY
- SSHÂ® Tectiaâ„¢
- VanDykeÂ® SecureCRTÂ®
- SSHTerm for Windows
- OpenSSH

# Secure Copy

The Local Manager can use Secure Copy (SCP) to copy files to and from a server. Based on the Secure Shell framework, SCP can be used via the **copy**, **update**, **export**, and **backup** commands.

# FTP

The Local Managerâ€™s FTP client is used by the **copy** command, export, archive, and backup. FTP is much less secure than SCP and should be used only in completely trusted networks.

The Local Managerâ€™s FTP server is used to transfer files to network devices that support it on TCP port 21. The Local Manager limits connections to specific IP addresses documented as device management IP addresses. The FTP server is only available during automated file transfer operations or if manually initiated during terminal pass-through. The server process is automatically terminated to limit possible security exposure.

# TFTP

Like the FTP server, the Local Managerâ€™s TFTP server is available only during automated file transfers between network devices and the Local Manager and on manual activation on UDP Port 69. **It is not limited to IP addresses**; it limits possible security exposure by specifically naming files.

# SFTP

Like the FTP server, the Local Managerâ€™s SFTP server is available only during automated file transfers between network devices and the Local Manager and on manual activation. **It is not limited to IP addresses**.

# Telnet access

[Telnet](https://uplogix.com/docs/local-manager-user-guide/security/telnetTelnet "Telnet") access to the Local Manager may be enabled, allowing clear-text clients to access the CLI. Port 23 is used by default. After enabling Telnet access, a reboot of the Local Manager is required.

# Modem access

Optional modem teletype (TTY) access is available if configured to provide single user dial-in access to the command line with support for encryption. Uplogix recommends using the Local Managerâ€™s outbound PPP/VPN service to reduce the security risks associated with dial-in modems.

By default, the modem does not answer incoming calls.

# Console access

An on-board RS-232 and mini USB console port is available for local access to the command line.

# The connect command

When logged in to a Local Manager, use the **connect** command to connect to another Local Managerâ€™s command line interface. While the protocol uses SSH, this command limits connectivity to only Local Managers, reducing overall security risk. Like all commands, this feature is limited to users authorized to execute it.