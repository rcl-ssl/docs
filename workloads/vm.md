---
title: Azure Virtual Machine
description: Using RCL SSL to automatically create, install and renew a SSL/TLS certificates in an Azure Virtual Machine
parent: Workloads
nav_order: 1
---

# SSL/TLS for Azure Virtual Machines 
**V7.1.0**

This workload is applicable for the **creation, installation and renewal** of a SSL/TLS certificate in Azure Virtual Machines (VM) (Linux or Windows) running a web server.

The web servers running in the VM may include : 

 - Apache
 - Apache Tomcat
 - Nginx
 - Microsoft IIS
 - Other web servers and hosting systems

# Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL SSL Portal by using any of the following options :

    - [Stand Alone](../portal/stand-alone.md) 
    - [Stand Alone SAN](../portal/stand-alone-san.md) 
    - [Azure DNS](../portal/azure-dns.md)
    - [Azure DNS SAN](../portal/azure-dns-san.md)

- The SAN options allow for two domains on a single certificate, whereas, the other option only allows one domain on the certificate

# Install the SSL/TLS Certificate in a Web Server

- Install the SSL/TLS Certificate in a web server running in the VM :

    - [Apache](../installations/apache.md)
    - [Apache Tomcat](../installations/apache-tomcat.md)
    - [NGINX](../installations/nginx.md)
    - [Microsoft IIS](../installations/iis.md)
    - [Other web servers and hosting systems](../installations/web-servers.md)

# Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to renew the certificate.

## Manual Renewal - Stand Alone and Stand Alone SAN

- Delete the SSL/TLS certificate in the RCL SSL Portal just before it expires
- Create a new certificate using the 'Stand Alone' or 'Stand Alone SAN' option
- Remove the old certificate and re-install the new one in your web server

## Manual Renewal - Azure DNS and Azure DNS SAN

- In the Certificate List, click on **Manage > Update**
- Then update the certificate
- Remove the old certificate and re-install the new one in your web server

## Automatic Renewal with RCL SSL HTTP AutoRenew

Automatic certificate renewal and installation in a web server hosted in a VM is supported with the [HTTP Challenge Type](../portal/stand-alone.md#completing-the-http-challenge) using [RCL SSL Http AutoRenew](../httpautorenew/httpautorenew.md). 

## Automatic Renewal with RCL SSL DNS AutoRenew

Automatic certificate renewal and installation in a web server hosted in a VM is supported using [RCL SSL DNS AutoRenew](../dnsautorenew/dnsautorenew.md). 


