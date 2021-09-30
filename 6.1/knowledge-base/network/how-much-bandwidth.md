During normal operation, the Local Manager is using network bandwidth for Heartbeat and Archive.

* Local Managers in minimal heartbeat use approximately 4KB every 30 seconds, or 480KB/hr.
* Local Managers in full heartbeat use approximately 40KB every 30 seconds, or 4MB/hr.

By default, Local Managers will archive large files to the Control Center every hour. These files include session logs, device configurations, and configuration backups. The size of the archive file will depend on the usage level of the appliance.

* A generally idle Local Manager may only send 5KB/hr.
* A heavily used Local Manager may send up to 1MB/hr.

Local Managers not under management by a Control Center may still use network bandwidth if the export function is enabled. These exports may use up to ~4MB/hr.

**Bottom Line:** Each Local Manager may send between 0.5MB to 10MB per hour depending on port density, settings, and system load.