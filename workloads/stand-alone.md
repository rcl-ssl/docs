---
title: Apache,Tomcat,NGINX,IIS,etc. 
description: Using RCL SSL to create and install SSL/TLS certificates
parent: Workloads
nav_order: 1
---

# SSL/TLS for Single-Instance Azure VM 
**V7.1.0**

This workload is applicable for the **creation, installation and renewal** of a SSL/TLS certificate in a Single-Instance Azure VM (Linux or Windows) running a web server.

The web servers may include : 

 - Apache
 - Apache Tomcat
 - Nginx
 - Microsoft IIS
 - Other web servers and hosting systems

# STEPS

## Step 1 : Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL SSL Portal by using either the :
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

### 3.1 Manual Renewal

- Delete the SSL/TLS certificate in the RCL SSL Portal just before it expires
- Create a new certificate using the 'Stand Alone' or 'Stand Alone SAN' option
- Remove the old certificate and re-install the new one in your web server

### 3.2 Automatic Renewal

Automatic certificate renewal is supported with the [HTTP Challenge Type](../portal/stand-alone.md#completing-the-http-challenge) using [RCL SSL Http AutoRenew](../httpautorenew/httpautorenew.md). 


