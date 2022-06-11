---
title: Stand Alone 
description: Using RCL to install SSL/TLS certificates
parent: Workloads
nav_order: 1
---

# Stand Alone Workload for SSL/TLS
**V6.0.10**

The stand alone workload is applicable for the **manual creation, installation and renewal** of a SSL/TLS certificate in a web server.

The web servers may include : 

 - Apache
 - Apache Tomcat
 - Nginx
 - Microsoft IIS
 - Other web servers and hosting systems

# STEPS

## Step 1 : Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the :
    - [Stand Alone](../portal/stand-alone.md) option
    - [Stand Alone SAN](../portal/stand-alone-san.md) option

- The Stand Alone option allows for one domain on a certificate, the SAN options allow for two domains on a single certificate.

## Step 2 : Install the SSL/TLS Certificate in a Web Server

- Install the SSL/TLS Certificate in a web server :
    - [Apache](../installations/apache.md)
    - [Apache Tomcat](../installations/apache-tomcat.md)
    - [NGINX](../installations/nginx.md)
    - [Microsoft IIS](../installations/iis.md)
    - [Other web servers and hosting systems](../installations/web-servers.md)

## Step 3 : Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to renew the certificate.

- Delete the SSL/TLS certificate in the RCL Portal
- Create a new certificate using the 'Stand Alone' or 'Stand Alone SAN' option
- Remove the old certificate and re-install the new one in your web server
