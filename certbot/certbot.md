---
title: RCL CertificateBot
description: RCL CertificateBot for automatic SSL/TLS certificate installation and renewal in Linux and Windows servers
has_children: true
nav_order: 8
---

# RCL CertificateBot
**V6.0.10**

RCL CertificateBot can be run as a Linux Daemon or a Windows Service in the web hosting machine for automatic certificate renewal. It is installed in the server hosting a website. It provides the following functionality :

- automatically renew certificates created in the RCL Portal
- save SSL/TLS certificates in the hosting machine for a web server to use 

The following web servers are supported:

- Apache
- Apache Tomcat
- NGINX
- IIS
- any server that configures SSL/TLS by referencing certificate files stored in the hosting machine

RCL CertificateBot will run every seven (7) days on the hosting machine and automatically renew and save certificates to the hosting machine. Web severs on the hosting machine will be configured to use theses certificates.