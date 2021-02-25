!DRAFT

# Overview

By default, the Uplogix Control Center does not ship with an HTTPS certificate, which often results in a strongly worded browser warning when you connect to it for the first time. Customers may choose to install their own HTTPS certificate, but if that is not an option, Let's Encrypt can be used instead.

* [Learn More about Let's Encrypt](https://letsencrypt.org/)

# Requirements

Let's Encrypt is not intended for servers in a private network with no access to the public internet. 

* UCC must have a publicly accessible IP address (direct, NAT, DMZ, etc.)
* Ports 80 and 443 must be visible to the internet
* DNS must be configured to resolve **acme-v02.api.letsencrypt.org**.
* **acme-v02.api.letsencrypt.org** must be reachable

# Configuration

Log into the UCC and become root.

Edit **/etc/sysconfig/embassy.overrides** and ensure the following property is set.

```
ACME_URL=https://acme-v02.api.letsencrypt.org/directory
```

Edit **/uplogix/embassy/data/www_csr.params** and ensure the following properties are set. Make sure to replace the example host names shown below with the correct UCC hostname and alternate hostnames, if any.

```
_csr_CN=hostname.example.com
_csr_SAN=hostname.example.com,another-hostname.example.com
```

# Verification

Once configuration is complete, run the following command to generate and import the certificate for tomcat. Note the time and date when the command finishes.

```
[root@UplogixControlCenter ~]# /uplogix/embassy/scripts/acmeCertificate.sh www
Generating RSA private key, 4096 bit long modulus (2 primes)
.................................................................................................................................................................................................................................................................................................................................................++++
.......................................................................................................................................................................................................................................................................++++
Generating new 2048-bit key pair.
Parsing account key...
Parsing CSR...
Found domains: hostname.example.com
Getting directory...
```

If no errors are encountered, restart UCC services.

```
[root@vUCC-Eval ~]# ucc restart
Shutting down Uplogix MatchMaker: er:                      [  OK  ]
Stopped Uplogix MatchMaker.
Updating settings in /usr/tomcat/webapps/ROOT/WEB-INF/classes/database.xml
Updating settings in /uplogix/envoy/config/oracleDatabase.xml
Updating settings in /uplogix/envoy/../matchmaker/config/database.xml
Updating ehcache file
Starting Uplogix Control Center:                           [  OK  ]
Starting Uplogix Migration:                                [  OK  ]
Starting Uplogix MatchMaker:                               [  OK  ]
```

Once the UCC has restarted, access the web interface using a browser and examine the certificate. Ensure the certificate is issued by Let's Encrypt. The Validity Period should approximately match when the acmeCertificate.sh script finished.

# Renewing

Let's Encrypt certificates are only valid for 90 days. You can renew them manually or through a cron job.