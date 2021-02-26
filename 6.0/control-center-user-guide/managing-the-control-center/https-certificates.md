This article describes the installation of an HTTPS certificate for deployments that require it. Although the process is simple, sometimes CSRs and Certs can be tricky, so be sure to contact Uplogix Support if you have any questions or encounter any issues.

## Step 1

Log into your Control Center, become root, and shut down the *tomcat* and *migration* services.

```
djones@central:~$ ssh emsadmin@172.30.161.18
emsadmin@172.30.161.18's password: 
[emsadmin@ems18 ~]$ sudo su - 
Password:
[root@ems18 ~]# service tomcat stop
[root@ems18 ~]# service migration stop
```

## Step 2

Run **/uplogix/embassy/scripts/generateCertificateSigningRequest.sh** and fill in the prompts. Use the IP address or Hostname of the Control Center as the **Common Name**.

## Step 3

Give the output of the script to your certificate authority for signing.

## Step 4

Paste the signed certificate into a file on the Control Center. In this example, we'll call it www.pem.

```
[root@ems18 ~] vi www.pem
```

## Step 5

Run: **/uplogix/embassy/scripts/importCertificate.sh www www.pem**

Substitute your filename for www.pem. The script will place the final files in the right locations.

## Step 6

Restart the *tomcat* and *migration* services with the **service* command.

```
[root@ems18 ~]# service tomcat start
[root@ems18 ~]# service migration start
```

## Complete

Log into the Control Center and verify the certificate has been installed correctly.