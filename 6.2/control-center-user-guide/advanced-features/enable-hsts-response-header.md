# Overview
As of LMS version 6.0.1, the HTTP Strict Transport Security (HSTS) response header is not enabled by default. If this feature is required by a security audit or vulnerability assessment, it can be enabled manually.

**This article is only applicable to LMS version 5.5.x and 6.0.x**.

# Instructions
To enable HSTS, you will need root access to your Control Center. SSH to the UCC as emsadmin and [become root](/docs/control-center-user-guide/managing-the-control-center/becoming-root).

## Configure HTTPS Certificates

Before proceeding, ensure you have already added HTTPS certificates by following this guide: [HTTPS Certificates](https://uplogix.com/docs/control-center-user-guide/managing-the-control-center/https-certificates)

<div class='danger' />Enabling HSTS **without** an HTTPS certificate will prevent you from bypassing the security warnings in modern browsers. Only enable this setting if you have an HTTPS certificate installed.</div>

## Modify embassy.overrides

Use vi to edit **/etc/sysconfig/embassy.overrides** and add the following line. Do not modify any other lines.

```
HSTS_ENABLE=true
```

The final result may look like this:

```
[root@uplogix-control-center ~]# cat /etc/sysconfig/embassy.overrides 
RAM=8
DISKS=6
HSTS_ENABLE=true
```

## Reorder entries in web.xml

Use vi to edit **/usr/tomcat/webapps/ROOT/WEB-INF/web.xml**.

Find the section that looks like this and references Security Filter and HttpHeaderSecurityFilter:

```
<!-- *** This needs to be the first filter-mapping *** -->
  <filter-mapping>
    <filter-name>Security Filter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  <filter-mapping>
    <filter-name>HttpHeaderSecurityFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

Swap the order of these two filter-mapping entries so it looks like this:

```
<!-- *** This needs to be the first filter-mapping *** -->
  <filter-mapping>
    <filter-name>HttpHeaderSecurityFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>

  <filter-mapping>
    <filter-name>Security Filter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
```

## Restart Tomcat
Use the **service tomcat restart** command to restart tomcat service.

```
[root@uplogix-control-center ~]# service tomcat restart
Updating settings in /usr/tomcat/webapps/ROOT/WEB-INF/classes/database.xml
Updating settings in /uplogix/envoy/config/oracleDatabase.xml
Updating settings in /uplogix/envoy/../matchmaker/config/database.xml
Updating ehcache file
Starting Uplogix Control Center: ter:                      [  OK  ]
[root@uplogix-control-center ~]# 
```

# Retest

Run your vulnerability assessment again and ensure HSTS is present or no longer flagged.

For assistance, please contact Uplogix Support.


