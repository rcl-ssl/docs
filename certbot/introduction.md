---
title: Introducing the CertificateBot
description: RCL SSL CertificateBot for automatic SSL/TLS certificate installation and renewal in Linux and Windows servers
parent: RCL SSL CertificateBot
nav_order: 1
---

# Introduction
**V7.0.0**

RCL SSL CertificateBot is installed in a hosting machine. 

It allows for automatic renewal of SSL/TLS certificates and installation of certificates in the hosting machine for a **web server** to use.

## Linux Server

RCL SSL CertificateBot runs as a **Daemon** in a Linux Server.

## Windows Server

RCL SSL CertificateBot runs as a **Windows Service** in a Windows Server.

## How it Works

- The application will request a list of certificates in a user's subscription in the RCL SSL Portal
- It will look for certificates in the list that are specified to be 'included in the hosting machine'. If it finds a specified certificate, it will save the certificate in the hosting machine
- If a certificate is about to expire, it will be scheduled for renewal, and subsequently saved to the hosting machine the next time the process is run
- The web server will be automatically configured to use the SSL/TLS certificate that was saved to the hosting machine

This entire process is repeated every seven (7) days to ensure the automatic renewal and installation of certificates.

## Web Servers
Web servers can use the certificates saved in the Windows or Linux hosting machine.

The following web servers are supported:

- Apache
- Apache Tomcat
- NGINX
- IIS
- any server that configures SSL/TLS by referencing certificates files stored in the server

## Important
**Please do no use the [RCL SSL AutoRenew Function](../autorenew/autorenew.md) if you are using CertificateBot. This may result in unexpected behavior and certificates may not be automatically updated in the hosting machine.**

## Next Steps

- [RCL SSL CertificateBot - Linux Service](./linux-daemon)
- [RCL SSL CertificateBot - Windows Service](./windows-service)
- [RCL SSL CertificateBot - IIS](./iis.md)


