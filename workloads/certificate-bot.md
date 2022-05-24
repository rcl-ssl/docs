---
title: Automatic Renewal
description: Automatically create, install and renew a SSL/TLS certificates in Web Servers
parent: Workloads
nav_order: 4
---

# Automatic Renewals and Installations

**V6.0.10**

This workload allows for the **automatic installation and renewal** of a SSL/TLS certificate in web servers.

The following web servers are supported:

- Apache
- Apache Tomcat
- NGINX
- any server that configures SSL/TLS by referencing certificate files stored in the server

# STEPS

## Step 1 : Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the:
    - [Azure DNS](../portal/azure-dns.md) option
    - [Azure DNS SAN](../portal/azure-dns-san.md) option

## Step 2 : Automatically Install the Certificate

- After certificate creation, install and configure the [RCL CertificateBot](../certbot/certbot.md) in your hosting machine (server) 
- RCL CertificateBot can in installed as a [Linux Daemon](../certbot/linux-daemon.md) on a **Linux Server** or a [Windows Service](../certbot/windows-service.md) in a **Windows Server**  
- RCL CertificateBot will automatically download and save certificates in your hosting machine for the web server to use

## Step 3 : Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. 

- RCL CertificateBot will look for certificates about to expire on a weekly basis and automatically schedule certificates for renewal 
- Renewed certificates will be downloaded and stored on your server where they can be referenced by the web servers hosting your website