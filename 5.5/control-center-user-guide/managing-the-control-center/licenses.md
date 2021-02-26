<!-- 5.4 -->
<div class='ucc' />Administration > Licenses</div>
# Overview

Licenses extend the functionality of the Uplogix Control Center and allow:

* Managing more Local Managers
* Enabling SLV
* Enabling Virtual Ports

Most licenses are installed prior to shipment, but if you need to update the license later, you can do so from the Control Center's web interface.

![UCC Licenses Page](http://uplogix.com/support/docs/img/5.4/uplogix-control-center-administration-licenses.png)

# Getting your license

If you do not have an updated or recently purchased license, Uplogix Support can provide it to you.

A typical UCC license:

```
---- LICENSE ----
ems.envoys=1
slv.envoys=1
virtual.ports=1
slv.expirationDate=01/01/1000 00:00:00
customer=Uplogix
--- SIGNATURE ---
MIAGCSqGSIb3DQEHAqCAMIACAQExDzANBglghkgBZQMEAgMFADCABgkqhki
G9w0BBwGggCSAAAAAAAAAoIIDCDCCAwQwggHsoAMCAQICBPJujDcwDQYJKo
w0wNTA5MjMwMDE5MzhaFw0xMDA5MjQwMDE5MzhaMBIxEDAOBgNVBAMTB3Vw
bG9naXgwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDbjoUfd22
wX3F+hhG/bqxK5bHA9EZczvJQQuf4Jrqza8+6rAqSxBoBo7cj6lNuyhU9KW
P0hLY7YnoLOI+fPzWDuNEOLbuOAIa2/bqkRASRUOpiKjOjqnR7MMg82G5eI
moFa9VG2w63Y6bT577ASJH5vNdAkr7KYaZ/lAaTaqPT6XlsbgZTzJvC46FD
ZIhvcNAQENBQAwHjEcMBoGA1UEAxMTVXBsb2dpeCBzZWxmLXNpZ25lZDAeF
SxLt8swPQZzV9O5lWXBKmQ89Jo+KBjeO4HPiP3VooU+nmEVDzAF3Vehhl/E
Lp21yqqY6gnDOiQIsZO8FSpKShsZPJqRa9wTIfAgMBAAGjVjBUMAwGA1UdE
wEB/wQCMAAwDgYDVR0PAQH/BAQDAgWgMBYGA1UdJQEB/wQMMAoGCCsGAQUF
BwMBMBwGA1UdEQQVgRNqZG9sbGFyQHVwbG9naXguY29tMA0GCSqGSIb3DQE
BDQUAA4IBAQCwVXi5prlNyY0SB1urc9dPag8qWRV76OYWnN4TXl2dfRN9KM
94ZAJ93ZdUOFGPm0Yh16NMNQSmuS1qM6kmKEK85BHo06WvjCUluurXa/CND
Us8e5AnfNdq2eOnFpFvyP5KnCMzQEQXpVRhJvDVrQUWldjES6GQpjOqrN4A
KIcJllUdcwN5c7i04QvoMTYUwiZxocBfdWuQdIHBED6PDws25l5VuTYFUcL
YNUd57VRRBBGmdUt8Afp8/lfRZ9R79lyUbn15b7e9CD4Py6zxt/Qzpb8XNn
t+vZBGF4GJzYZH2G4XHPlwK2JkusVcl7G7UjgfjYhFtll6KEe4t2Fg9iPKX
/O/kJB4bhujuBV5uXHZKbFKIf8vPvdATaEFfMfEi8QePJTNxP1qnaYQVRlM
YIB3TCCAdkCAQEwJjAeMRwwGgYDVQQDExNVcGxvZ2l4IHNlbGYtc2lnbmVk
AgTybow3MA0GCWCGSAFlAwQCAwUAoIGJMBgGCSqGSIb3DQEJAzELBgkqhki
cNAQkEMUIEQFjenUD9/ZrjYvKz2hoNLPPtZBmf8iFohvkodD3PWe7ic2DVp
M9cqgpP8DOKllqASaYqQHF2cSh0ZbGtt9qYJXIwDQYJKoZIhvcNAQEBBQAE
ggEAZgIQsYmfpB8wK4BSNdVAY3O50+iPhlsAIi6ZoY7eQtXgTRe1q2ypVSL
q4il3LtddudboWQKRJFQx3tff4niEXQzTDv1vHlJwN1Xlanih7ojl2VjXLM
G9w0BBwEwHAYJKoZIhvcNAQkFMQ8XDTExMDYwNjIyMDAwNFowTwYJKoZIhv
putRXLH8MapnTYHJjNaA+uuYu4j36JXW2yys9YqW8RdNU/H5dVIe9ekStev
SxlAiwqY8W0E/mVGEn87jlTbW7UY/8vvLGJY+gSVxizltQqgC+k4wcQvySe
wvPcKizBz846hS2HCOIiTzetlL9SwisB7zCbVM9SOsb4m2StZpwAAAAAAAA==
-----------------
```

# Installing a license

Log into your Control Center as a user with admin privileges on the server resource. Click *Administration* and then *Licenses*.

Click *Add*.  

Paste in the entire contents of the license.

![UCC Licenses Page - Installing](http://uplogix.com/support/docs/img/cc-user-guide/ucc_licenses_adding.png)

Click *Save*. 

> If the license is not valid, or if it was pasted incorrectly, you will be presented with a *License is not valid* message.

# Verifying

If the license was valid, you will be returned to the Licenses page. You should see your license listed.

![UCC Licenses Page - Viewing](http://uplogix.com/support/docs/img/cc-user-guide/ucc_licenses_added.png)

If necessary, you can remove or view the certificate of a license.

# Choose Systems

If your license included Service Level Verification (SLV) support, the *Choose Systems* button will be enabled.

![UCC Licenses Page - Choose Systems](http://uplogix.com/support/docs/img/cc-user-guide/ucc_licenses_choose_systems.png)

Check the box next to each Local Manager on which you'd like to enable SLV and click *Save* when done.