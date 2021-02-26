# Overview
Zero Touch Deployment enables the automatic configuration of Local Managers via DHCP. A factory fresh Local Manager will use DHCP and DNS to automatically find and begin communicating with the Uplogix Control Center (UCC). Once a Local Manager is communicating with the UCC, a network administrator can move the Local Manager into an inventory group and begin configuring it. This functionality eliminates the need to preconfigure a Local Manager before sending it to a remote site, as well as the need to have technical assistance on-site when deploying a new Local Manager.

# Dynamic Host Control Protocol (DHCP)

The Local Manager (LM) will attempt to DHCP an IP address for its management Ethernet interface on first boot. In addition to using DHCP to automatically configure its Ethernet management interface, it will use DNS, domain, and NTP information (if present) to configure network settings and attempt to automatically find and begin communicating with the UCC.

## DNS Servers

If a list of DNS servers is provided to the Local Manager via DHCP, it will automatically configure itself to use those servers for name resolution unless automatic DNS configuration is disabled.

## DNS Domain

If a domain or list of domains is provided to the Local Manager via DHCP and the management server (UCC) setting is set to automatic configuration (the default setting), the Local Manager will attempt to use the domain(s) and DNS servers to resolve the UCC IP address by querying the DNS server for a TCP "uplogix" service (i.e. SRV record).  Here is an example of a SRV record for the Uplogix Control Center service:

```
_uplogix._tcp.yourcompany.com. 3600 IN SRV 0 5 8443 ucc.yourcompany.com.
```

### SRV Record Format
| Setting | Description |
| - | - |
| service | The name of the Uplogix service - should be set to "uplogix" - this field should begin with an underscore and end with a dot |
| protocol | The Uplogix service transport protocol - should be set to "TCP" - this field should begin with an underscore and end with a dot | 
| name | The domain name for which this service record is valid, ending in a dot. |
| TTL | This is the standard DNS time to live - set to 1 hour in this example |
| class | This is the standard DNS class field (this is always IN). |
| Record type | Since this is a service record, it should be set to "SRV" |
| priority | The priority of the target host, lower value means more preferred. |
| weight | A relative weight for records with the same priority, higher value means more preferred. |
| port | The TCP port on which the service is to be found - the Uplogix Control Center uses TCP port 8443. |
| target | The canonical hostname of the machine providing the service, ending in a dot. |

If the Local Manager fails to resolve the UCC name querying for a service record, it will attempt to resolve the UCC IP address by querying for an A-record using the following name convention: *uplogix-control-center.<DHCP=provided domain>*. If the Local Manager cannot resolve the UCC IP address, it will begin traversing the search domain, attempting to resolve the UCC name all the way back to the root domain.

## NTP Servers

If a list of NTP servers is provided to the Local Manager via DHCP, it will automatically configure itself to use those servers to set and correct its clock unless automatic NTP configuration is disabled.

# Automatic Management Server Configuration Without DHCP

While true Zero Touch Deployment requires DHCP, automatic server configuration can be configured without using DHCP for the case where you want the Local Manager to automatically find its Uplogix Control Center.  In this case, when you run the **config system ip** command to configure a static management IP address for the LM, be sure to configure at least one DNS server and a domain. For example:

```
[admin@UplogixLM]# config system ip
--- Existing Values --- 
Use DHCP: Yes 
Management IP: 0.0.0.0
Host Name: UplogixLM
Subnet Mask: 255.255.255.0 
Broadcast Address: 0.0.0.255 
Default Route: 0.0.0.0 
Speed/duplex: auto: 1000full
MAC Address: 00:0F:2C:00:CC:C6 
Bonding Link: yes
[E1] Primary Ethernet Link: yes (bonded active)
[E2] Auxiliary Ethernet Link: no (bonded)
[E3] Internal SFP Ethernet Link: no (bonded)
Change these? (y/n) [n]: y
--- Enter New Values --- 
Use DHCP: (y/n) [y]: n
Management IP: [0.0.0.0]: 198.51.100.4
Host Name: [UplogixLM]: 
Subnet Mask: [255.255.255.0]: 
Default Route: [0.0.0.0]: 198.51.100.254
speed/duplex: [auto:1000full]: 
Use DNS (y/n) [y]: 
Automatically configure DNS (y/n) [y]: n
DNS Server IP 1: 172.30.4.252
DNS Server IP 2: 172.30.4.253 
Domain Search: yourcompany.com
Warning: Remote connections may be lost if you commit changes. 
Do you want to commit these changes? (y/n): y
```