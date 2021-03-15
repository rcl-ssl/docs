---
title: Introduction
description: RCL CertificateBot for automatic SSL/TLS certificate installation and renewal in Windows and Linux servers
parent: CertificateBot
nav_order: 1
---

# Introduction

RCL CertificateBot is installed in a server running a website. It allows for automatic renewal of SSL/TLS certificates and installation of certificates in the server.

## Windows Server

RCL CertificateBot runs as a **Windows Service** in a Windows Server.

## Linux Server

RCL CertificateBot runs as a **Daemon** in a Linux Server.

## How it Works

- The application will request a list of certificates in a user's subscription in the RCL Portal
- It will look for certificates in the list that are flagged 'to-be-saved-in-the-server'. If it finds a certificate, it will save the certificate in the server.
- Certificates that are saved in the server will then be flagged as 'saved-in-the-server'
- The application will then send a request to to renew certificates in a user's subscription. This request is sent every four (4) days
- If a certificates is about to expire, it will be renewed and flagged as 'to-be-saved-in-the-server'

This entire process is repeated every four (4) days to ensure the automatic renewal and installation of certificates in a server.

## Web Servers
Web servers can use the certificates saved in the Windows or Linux server.

The following web servers are supported:

- Apache
- Apache Tomcat
- NGINX
- any server that configures SSL/TLS by referencing certificates files stored in the server

## Next Steps

- [RCL CertificateBot - Windows Service](./windows-service)
- [RCL CertificateBot - Linux Service](./linux-daemon)

