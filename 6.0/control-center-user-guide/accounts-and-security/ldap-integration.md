# Overview

To authenticate users against an LDAP server, such as Microsoft Active Directory, the Uplogix Control Center (UCC) or Uplogix Local Manager (LM) must connect through a RADIUS server, which brokers the connection to the LDAP server. This document explains how to configure the FreeRADIUS service to run on a UCC.

After FreeRADIUS is configured, the UCC and LMs can be set to use the RADIUS / LDAP service for user authentication. The UCC and LMs can also be configured to automatically create users and assign them to Uplogix groups that match their LDAP group membership.

# Requirements

* Uplogix Control Center running LMS version 5.4 or higher
* LDAP Server (Microsoft Server 2012 has been tested)
* Root access to the Control Center's Linux operating system

# Control Center Configuration

## Testing

During testing, you may want to use the following command to start FreeRADIUS in debug mode:

```
/usr/sbin/radiusd -X
```

## Clients

Edit /etc/raddb/clients.conf and add an entry to the bottom of the file with the IP address or network of the Control Center. In this example, the Control Center is 198.51.100.1.

```
client 198.51.100.1 {
# # secret and password are mapped through the "secrets" file.
secret = password
shortname = TESTUCC
}
```

Or to just specify the network:

``` 
client 198.51.100.0/24 {
secret = uptime
shortname = insideUplogix
}
```

## Uplogix Dictionary

Add the following lines to /usr/share/freeradius/dictionary.uplogix:

```
VENDOR          Uplogix                 10243

BEGIN-VENDOR    Uplogix

ATTRIBUTE       Uplogix-Version                         1       string

ATTRIBUTE       Uplogix-User-Groups                     3       string
ATTRIBUTE       Uplogix-CLI-Command                     4       string
ATTRIBUTE       Uplogix-Envoy-Serial                    5       string
ATTRIBUTE       Uplogix-Task-Id                         6       string

ATTRIBUTE       Uplogix-TEMP                            98      string

ATTRIBUTE       Uplogix-GROUP1                          81      string
ATTRIBUTE       Uplogix-GROUP2                          82      string
ATTRIBUTE       Uplogix-GROUP3                          83      string
ATTRIBUTE       Uplogix-GROUP4                          84      string
ATTRIBUTE       Uplogix-GROUP5                          85      string
ATTRIBUTE       Uplogix-GROUP6                          81      string
ATTRIBUTE       Uplogix-GROUP7                          82      string
ATTRIBUTE       Uplogix-GROUP8                          83      string
ATTRIBUTE       Uplogix-GROUP9                          84      string
ATTRIBUTE       Uplogix-GROUP10                        85      string
ATTRIBUTE       Uplogix-GROUP11                        81      string
ATTRIBUTE       Uplogix-GROUP12                        82      string
ATTRIBUTE       Uplogix-GROUP13                        83      string
ATTRIBUTE       Uplogix-GROUP14                        84      string
ATTRIBUTE       Uplogix-GROUP15                        85      string


END-VENDOR      Uplogix
```

Add the following line to /usr/share/freeradius/dictionary:

```
$INCLUDE dictionary.uplogix
```

## Attribute Map

Add the following lines to /etc/raddb/ldap.att

```
replyItem Uplogix-TEMP memberOf +=
```

## RADIUS Configuration

Replace the contents of /etc/raddb/radiusd.conf with the following.

You will need to update the following fields for your LDAP server:

* server
* identity
* password
* basedn

```
prefix = /usr
exec_prefix = /usr
sysconfdir = /etc
localstatedir = /var
sbindir = /usr/sbin
logdir = ${localstatedir}/log/radius
raddbdir = ${sysconfdir}/raddb
radacctdir = ${logdir}/radacct
confdir = ${raddbdir}
run_dir = ${localstatedir}/run/radiusd
db_dir = ${localstatedir}/lib/radiusd

libdir = /usr/lib
pidfile = ${run_dir}/radiusd.pid
user = radiusd
group = radiusd
max_request_time = 30
delete_blocked_requests = no
cleanup_delay = 5
max_requests = 1024
listen { 
	type = auth
	ipaddr = * 
	port = 0
}
listen { 
	type = acct	
	ipaddr = *
	port = 0
}

hostname_lookups = no
allow_core_dumps = no
regular_expressions     = yes
extended_expressions    = yes

log {
	destination = files
	file = ${logdir}/radius.log
	syslog_facility = daemon
	stripped_names = no
	auth = no
	auth_badpass = no
	auth_goodpass = no
}

usercollide = no
lower_user = no
lower_pass = no
nospace_user = no
nospace_pass = no
checkrad = ${sbindir}/checkrad
security {
        max_attributes = 200
        reject_delay = 1
        status_server = no
}
proxy_requests  = yes
$INCLUDE  ${confdir}/proxy.conf
$INCLUDE  ${confdir}/clients.conf
snmp    = no
#$INCLUDE  ${confdir}/snmp.conf
thread pool {
        start_servers = 5
        max_servers = 32
        min_spare_servers = 3
        max_spare_servers = 10
        max_requests_per_server = 0
}
modules {
        ldap {
                # With CentOS 6 (freeradius 2.2.6), if you use
                # start_tls, you need to use the hostname, so it will
                # match the certificate of the server
				        server = "203.0.113.14"
 				        identity = "CN=Administrator,CN=Users,DC=doc,DC=uplogix,DC=com"
                password = "strong_generated_password"
                basedn = "CN=Users,DC=doc,DC=uplogix,DC=com"
                filter = "(sAMAccountName=%{Stripped-User-Name:-%{User-Name}})"
                start_tls = no
                ldap_debug = 0xffff
                ldap_connections_number = 5
                edir_account_policy_check=no
                timeout = 4
                timelimit = 3
                net_timeout = 1
        }
        preprocess {
                huntgroups = ${confdir}/huntgroups
                hints = ${confdir}/hints
                with_ascend_hack = no
                ascend_channels_per_line = 23
                with_ntdomain_hack = no
                with_specialix_jetstream_hack = no
                with_cisco_vsa_hack = no
        }
        detail {
                detailfile = ${radacctdir}/%{Client-IP-Address}/detail-%Y%m%d
                detailperm = 0600
        }
}
instantiate {
}
authorize {
        preprocess
	ldap
}
authenticate {
        Auth-Type LDAP {
                ldap
        }
}
preacct {
        preprocess
}
accounting {
        detail
}
session {
}
post-auth {


                # strip DN, CN, etc... - AT

                if ("%{reply:Uplogix-TEMP[0]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP1 := "%{1}"
                                        }
                        }
                }



                if ("%{reply:Uplogix-TEMP[1]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP2 := "%{1}"
                                        }
                        }
                }


                if ("%{reply:Uplogix-TEMP[2]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP3 := "%{1}"
                                        }
                        }
                }


                if ("%{reply:Uplogix-TEMP[3]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP4 := "%{1}"
                                        }
                        }
                }


                if ("%{reply:Uplogix-TEMP[4]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP5 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[5]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP6 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[6]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP7 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[7]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP8 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[8]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP9 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[9]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP10 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[10]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP11 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[11]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP12 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[12]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP13 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[13]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP14 := "%{1}"
                                        }
                        }
                }

if ("%{reply:Uplogix-TEMP[14]}" =~ /(.*),CN=Users,DC=doc,DC=uplogix,DC=com$/) {
                        if ("%{1}" =~ /CN=(.*)/) {
                                        update reply {
                                            Uplogix-GROUP15 := "%{1}"
                                        }
                        }
                }




        update reply {


                Uplogix-User-Groups := " %{reply:Uplogix-GROUP1} ,  %{reply:Uplogix-GROUP2} , %{reply:Uplogix-GROUP3} , %{reply:Uplogix-GROUP4} , %{reply:Uplogix-GROUP5}"

                Uplogix-TEMP !* ANY
                Uplogix-GROUP1 !* ANY
                Uplogix-GROUP2 !* ANY
                Uplogix-GROUP3 !* ANY
                Uplogix-GROUP4 !* ANY
                Uplogix-GROUP5 !* ANY
                Uplogix-GROUP6 !* ANY
                Uplogix-GROUP7 !* ANY
                Uplogix-GROUP8 !* ANY
                Uplogix-GROUP9 !* ANY
                Uplogix-GROUP10 !* ANY
                Uplogix-GROUP11 !* ANY
                Uplogix-GROUP12 !* ANY
                Uplogix-GROUP13 !* ANY
                Uplogix-GROUP14 !* ANY
                Uplogix-GROUP15 !* ANY


        }




}pre-proxy {
}
post-proxy {
}
```
	
## TLS Configuration (optional)

To configure the FreeRADIUS server to use an encrypted connection, the /etc/raddb/radiusd.conf file must use a hostname to connect to the LDAP server, and it must have the following line changed to the following:

```
start_tls = yes
```

The next line after "start_tls = yes" must be the following:

```
tls_require_cert = "demand"
```

Edit /etc/openldap/ldap.conf, comment out TLS_CACERTDIR and add the TLS_CACERT location as follows (replacing the example with the certificate to be used):

```
#TLS_CACERTDIR /etc/openldap/certs
TLS_CACERT /etc/openldap/certs/WIN-243G5KGAVTH.pm.doc.uplogix.com.pem
TLS_REQCERT DEMAND
```

View the LDAP server certificate with the following command, selecting the CA certificate that signed the certificate that will be used by the LDAP server for encryption, and putting the certificate in the file listed above (ie - /etc/openldap/certs/WIN-243G5KGAVTH.pm.doc.uplogix.com.pem):

```
openssl s_client -connect WIN-243G5KGAVTH.pm.doc.uplogix.com:636 -showcerts
```

## Control Center AAA Settings Configuration

Navigate to Administration > AAA Settings on the Control Center and set the following values:

* Authentication Type: RADIUS
* Authentication Method: PAP
* Cache Passwords: Yes
* Fail over to Local: Yes
* Authentication Servers
	* IP: IP Address of the UCC
	* Port: 1812
	* Secret: same secret as above in Client Settings

# Local Manager Configuration

If left unconfigured, Local Managers will authenticate users based on the passwords cached when the user last logged into the Control Center. 

To have all Local Managers authenticate directly with the LDAP server via the FreeRADIUS proxy, return to the Administration > AAA Settings page and check the box at the bottom for **Force settings to all appliances in hierarchy**. Click *Save*.

Optionally, AAA Settings can be configured at both the Inventory Group or Local Manager level in the hierarchy. Use the same settings from **Control Center AAA Settings Configuration** above.

# Finishing up
If FreeRADIUS is still running in debug mode, use the following command to clear the debug flag and run in normal mode:

```
[root@UplogixControlCenter ~]# service radiusd restart
Stopping radiusd:                                          [  OK  ]
Starting radiusd:                                          [  OK  ]
```

To configure FreeRADIUS service to start when the UCC boots, use the **chkconfig** command:

```
[root@UplogixControlCenter ~]# chkconfig radiusd on
[root@UplogixControlCenter ~]# chkconfig --list | grep radiusd
radiusd         0:off   1:off   2:on    3:on    4:on    5:on    6:off
```

Congratulations! The Uplogix Control Center is now configured to work with LDAP.