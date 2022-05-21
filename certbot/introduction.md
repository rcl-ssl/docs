---
title: Introducing the CertificateBot
description: RCL CertificateBot for automatic SSL/TLS certificate installation and renewal in Linux and Windows servers
parent: RCL CertificateBot
nav_order: 1
---

# Introduction
**V6.0.10**

RCL CertificateBot is installed in a server running a website. It allows for automatic renewal of SSL/TLS certificates and installation of certificates in the hosting machine for a web server to use.

## Linux Server

RCL CertificateBot runs as a **Daemon** in a Linux Server.

## Windows Server

RCL CertificateBot runs as a **Windows Service** in a Windows Server.

## How it Works

- The application will request a list of certificates in a user's subscription in the RCL Portal
- It will look for certificates in the list that are specified to be 'included in the server'. If it finds a specified certificate, it will save the certificate in the server
- The application will then send a request to to renew certificates in a user's subscription. 
- If a certificates is about to expire it will be scheduled for renewal, and subsequently saved to the server the next time the process is run

This entire process is repeated every seven (7) days to ensure the automatic renewal and installation of certificates in a server.

## Web Servers
Web servers can use the certificates saved in the Windows or Linux server.

The following web servers are supported:

- Apache
- Apache Tomcat
- NGINX
- any server that configures SSL/TLS by referencing certificates files stored in the server

## Important
**Please do no use the [RCL AutoRenew Function](../autorenew/autorenew.md) if you are using CertificateBot. This may result in unexpected behavior and certificates may not be automatically updated in the hosting machine.**

## Next Steps

- [RCL CertificateBot - Linux Service](./linux-daemon)
- [RCL CertificateBot - Windows Service](./windows-service)


