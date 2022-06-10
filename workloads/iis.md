---
title: SSL/TLS for IIS
description: Automatically create, install and renew a SSL/TLS certificates in IIS Web Server
parent: Workloads
nav_order: 5
---

# SSL/TLS for IIS

**V6.0.10**

This workload allows for the **automatic installation and renewal** of a SSL/TLS certificate in the IIS web server.

## Step 1 : Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the:
    - [Azure DNS](../portal/azure-dns.md) option
    - [Azure DNS SAN](../portal/azure-dns-san.md) option

## Step 2 : Automatically Install the Certificate

- After certificate creation, install and configure the [RCL CertificateBot for IIS](../certbot/iis.md) in your Windows hosting machine (server) 

- [RCL CertificateBot for IIS](../certbot/iis.md) will automatically download the certificate in the Windows hosting machine and install the certificate in the IIS web server

## Step 3 : Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. 

- [RCL CertificateBot for IIS](../certbot/iis.md) will look for certificates about to expire on a weekly basis and automatically schedule certificates for renewal 
- Renewed certificates will be downloaded and stored on your Windows server and are automatically installed in the IIS web server