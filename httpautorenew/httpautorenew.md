---
title: HTTP AutoRenew 
description: RCL SSL HTTP AutoRenew application for automatic SSL/TLS certificate installation and renewal in Linux and Windows servers
has_children: true
nav_order: 7
---

# RCL SSL HTTP AutoRenew
**V7.0.0**

RCL SSL HTTP AutoRenew can be run as a Linux Daemon or a Windows Service in the web hosting machine for automatic certificate renewal. It is installed in the hosting machine. It provides the following functionality :

- automatically renew certificates created in the RCL SSL Portal using the [Stand Alone](../portal/stand-alone.md)
(including [SAN](../portal/stand-alone-san.md)) option using the HTTP Challenge type
- save SSL/TLS certificates in the hosting machine for a **web server** to use 

The following web servers are supported:

- Apache
- Apache Tomcat
- NGINX
- IIS
- any server that configures SSL/TLS by referencing certificate files stored in the hosting machine

RCL SSL HTTP AutoRenew will run every seven (7) days on the hosting machine and automatically renew and save certificates to the hosting machine. Web severs on the hosting machine will be automatically configured to use theses certificates.