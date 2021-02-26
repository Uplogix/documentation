<!-- 5.4 -->
<div class='ucc'>Administration > Server settings > Mail Settings</div>

The Control Center can be configured to send alerts and reports by email. A mail server should be configured with a valid IP address and authentication settings. 

![Uplogix Control Center Mail Settings](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-server-settings-mail.png)

To verify the email settings are configured correctly, click *Send a Test Email* to open the test email form. At a minimum, provide a valid email address where the test message should be received. Click *Send Test Email* to send the message.

![Send a Test Email](http://uplogix.com/support/docs/img/cc-user-guide/image013.jpg)
 
Once finished making changes, click *Save*.

# Secure SMTP

The Uplogix Control Center uses SMTP email to send reports, alerts and SMS messages to other network management systems, end users and Local Managers.  The Control Center uses specific SMTP smart-hosts to navigate the email system in each deployment. In FIPS mode, when the Control Center must send encrypted mail to a mail server, SSL certificates are used to encrypt the communication with mail servers. This document describes the process of installing SSL certificates for encrypted Control Center communications.

##  Control Center CLI Configuration

Create the SSL certificates according to your organizationâ€™s requirements. Then, import the individual certificates into the Control Center. Each certificate must individually imported to be trusted.  The example below shows the process with Google mail servers.

### Log into the Control Center CLI 
Log into the Control Centerâ€™s command line and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root).

### Obtain Certificates from the Host

Execute the **openssl** command to the host and port to retrieve its public key.  This key will later be imported into the Control Center certificate store. 

> **NOTE:** If you resolve these via DNS use the fully qualified hostname instead of the IP address.  Port 587 is the default port for submission of email; encryption is enabled after the initial SMTP handshake.  Port 465 is a legacy port for SMTP over SSL.

```
[root@vUCC]# openssl s_client -connect 64.233.176.108:587 -starttls smtp
CONNECTED(00000003)
depth=3 /C=US/O=Equifax/OU=Equifax Secure Certificate Authority
verify return:1
depth=2 /C=US/O=GeoTrust Inc./CN=GeoTrust Global CA
verify return:1
depth=1 /C=US/O=Google Inc/CN=Google Internet Authority G2
verify return:1
depth=0 /C=US/ST=California/L=Mountain View/O=Google Inc/CN=smtp.gmail.com
verify return:1
---
Certificate chain
 0 s:/C=US/ST=California/L=Mountain View/O=Google Inc/CN=smtp.gmail.com
   i:/C=US/O=Google Inc/CN=Google Internet Authority G2
 1 s:/C=US/O=Google Inc/CN=Google Internet Authority G2
   i:/C=US/O=GeoTrust Inc./CN=GeoTrust Global CA
 2 s:/C=US/O=GeoTrust Inc./CN=GeoTrust Global CA
   i:/C=US/O=Equifax/OU=Equifax Secure Certificate Authority
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIEgDCCA2igAwIBAgIIGN+Ja//q0lAwDQYJKoZIhvcNAQELBQAwSTELMAkGA1UE
BhMCVVMxEzARBgNVBAoTCkdvb2dsZSBJbmMxJTAjBgNVBAMTHEdvb2dsZSBJbnRl
cm5ldCBBdXRob3JpdHkgRzIwHhcNMTUxMjEwMTgwMTA0WhcNMTYwMzA5MDAwMDAw
WjBoMQswCQYDVQQGEwJVUzETMBEGA1UECAwKQ2FsaWZvcm5pYTEWMBQGA1UEBwwN
TW91bnRhaW4gVmlldzETMBEGA1UECgwKR29vZ2xlIEluYzEXMBUGA1UEAwwOc210
cC5nbWFpbC5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCYfS+8
2iz5goB44H99Q0u2Z1iUIcDgEMrTLd3Ym8o2X15xcNSwL+ewBIkeNKZRf91djlrD
DkrHrWgagOdHrHrM5Nzvbj5fFTieqqRXpYN6Htb3QpsCyTy2FPoYs2GoxWe5UgVR
RKND+Ar/iBqPlKFQd1I7sdyINtXKiR3gq0A5vRfgcEHEVMn3Sa/wPGtFZUJr8s81
CHY+0uvOo0kroyoljjEd6BuMQQh18e2W5RkGILOGMIqTxHdA9HXKkizteo/zq+3K
JU2xFmla3aYVejT0u8BfU7/wEUVlHwFiLqWq298aUcTsFFxsFAYGGOzgN5CKpGO2
Zd2ZygmkvQLjs1z9AgMBAAGjggFLMIIBRzAdBgNVHSUEFjAUBggrBgEFBQcDAQYI
KwYBBQUHAwIwGQYDVR0RBBIwEIIOc210cC5nbWFpbC5jb20waAYIKwYBBQUHAQEE
XDBaMCsGCCsGAQUFBzAChh9odHRwOi8vcGtpLmdvb2dsZS5jb20vR0lBRzIuY3J0
MCsGCCsGAQUFBzABhh9odHRwOi8vY2xpZW50czEuZ29vZ2xlLmNvbS9vY3NwMB0G
A1UdDgQWBBQoJ1JkvEFvIU79/z3n7wV2QCSFVzAMBgNVHRMBAf8EAjAAMB8GA1Ud
IwQYMBaAFErdBhYbvPZotXb1gba7Yhq6WoEvMCEGA1UdIAQaMBgwDAYKKwYBBAHW
eQIFATAIBgZngQwBAgIwMAYDVR0fBCkwJzAloCOgIYYfaHR0cDovL3BraS5nb29n
bGUuY29tL0dJQUcyLmNybDANBgkqhkiG9w0BAQsFAAOCAQEAKqc27Z5PSyy17bDK
UnnAhajPmfAQJKJBOOUJcMXmnzNlDQeK4Mc2/WYukOD8nbfuksIkDwc69QmhuYgn
95WGcCN82bksI9uaQ6nazYZ0z2pbTwqUdR8t4B5rrZdUE5i/nUEaxRxhsaEGCb7R
dJy7C7L8Ch5SECBWzFjvnlH3Kvx3q9QtAXJVLcvgN7o69GCG0eb/jenD1dV8pxdq
oFAbJYhvWLxjtYrY366HDS2LXvRDQ4wDQepL7yDZ9ZZvxNie404sSplh8R9VWKfJ
5aPw2ZJPl3WAI39qbNpDhK+re6nclKQmxrsd+VUrDMi1LnwSb3X0ox7nm1KK0rKE
d4rTmw==
-----END CERTIFICATE-----
subject=/C=US/ST=California/L=Mountain View/O=Google Inc/CN=smtp.gmail.com
issuer=/C=US/O=Google Inc/CN=Google Internet Authority G2
---
No client certificate CA names sent
---
SSL handshake has read 3493 bytes and written 482 bytes
---
New, TLSv1/SSLv3, Cipher is AES128-SHA
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
SSL-Session:
    Protocol  : TLSv1
    Cipher    : AES128-SHA
    Session-ID: E52E74B11F26AAF5C305F4A8A52C1F1A3DD588F6D9093D505CAB804F816BC693
    Session-ID-ctx:
    Master-Key: 5B8B2C7CA41508A0495BC05BE183C15141064D80CE27C20B6E43F99FC0540D23        3865FDA8A3F41BE7F55E9F176D083F11
    Key-Arg   : None
    Krb5 Principal: None
    Start Time: 1450383243
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
250 SMTPUTF8
```

Send the **CTRL-C** command to break out of the openssl command. Copy the yellow highlighted certificate text into a file in the /root directory. Next, use vi to create a file with the contents of the certificate.

```
[root@vUCC]# vi google.pem
Press the letter â€˜iâ€™ to insert new text
```
 
Paste the highlighted text from, "----BEGIN CERTIFICATE -----" to, "-----END CERTIFICATE-----".

Hit [ESCAPE], and then type ZZ to save the file. You should return to the command line:

```
[root@vUCC-Eval ~]# vi google.pem
[root@vUCC-Eval ~]#
```

### Import the serverâ€™s public key

Import the certificate file into the certificate store using the utility

```
[root@UCC]# /uplogix/embassy/scripts/importServerCertificate.sh add 64.233.176.108 587 /root/google.pem

Initializing crypto
Reading file: /root/google.pem
Adding 64.233.176.108:587
[root@UCC]#
```

> **NOTE:** If a load-balanced server environment has many hosts servicing mail with individual host certificates, the serverâ€™s CA certificate must be imported.

The Control Center should now be configured to forward email to the SMTP smarthost.  Log into the browser interface of the Control Center as an administrative user. Send a test email to validate the configuration.