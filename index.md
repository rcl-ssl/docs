﻿---
title: Introduction
description: The RCL SSL client for Let's Encrypt allows you to create SSL/TLS certificates for your web sites / applications using the popular Let's Encrypt V2 API.
has_children: false
nav_order: 1
---

# Introduction
**V7.1.0**

The RCL SSL Client for *Let's Encrypt*<sup>TM</sup> allows you to create free SSL/TLS certificates for your web sites / applications using the popular *Let's Encrypt*<sup>TM</sup> V2 API.

![image](./images/portal/rcl_ssl_200.png)

Use the RCL SSL Portal and the various RCL SSL Apps to create and renew single or multiple-domain SSL/TLS certificates for your web sites / applications. The following domains are supported

- Naked apex domains (e.g. contoso.com)
- Sub-domains (e.g. store.contoso.com, www.contoso.com)
- Wild card domains (e.g. *.contoso.com) 
- Subject Alternative Name (SAN) mutli-domains (multiple domains in a single certificate) 

<sub>Let's Encrypt is a trademark of the [Internet Security Research Group](https://www.abetterinternet.org/). All rights reserved.</sub>

# RCL SSL Portal

The [RCL SSL Portal](../portal/portal) is the **primary application**. It is a SaaS application that you can [subscribe](./subscription/subscription.md) for in Microsoft Azure Marketplace.

![image](./images/portal/portal.PNG)

The RCL SSL Portal is a simple-to-use online Web UI and allows you to :

- Create [Single](../portal/stand-alone) and [Multi-Domain SAN](../portal/stand-alone-san) SSL/TLS certificates. You can download the certificates and manually install them in your web servers. It is ideal for web applications hosted in web servers (eg. Apache, Tomcat, NGINX, IIS, Express, etc.).

- Automatically create and install SSL/TLS certificates in Microsoft Azure Services such as [Azure Virtual Machines](./workloads/vm.md), [Azure Key Vault](./workloads/keyvault.md), [Azure Application Gateway](./workloads/appgateway.md) and [Azure App Services](./workloads/app-service.md).

# The Other RCL Apps

## RCL SSL AutoRenew Function

The [RCL SSL AutoRenew](/autorenew/autorenew) function is an Azure Function app that runs in an [Azure Consumption Plan](https://docs.microsoft.com/en-us/azure/azure-functions/consumption-plan). The primary purpose of the RCL SSL AutoRenew Function is to automate the renewal and installation of certificates created in the [RCL SSL Portal](./portal/portal.md) for an [Azure App Service](./portal/azure-appservice.md) or [Azure Key Vault](./portal/azure-keyvault.md) . The RCL SSL AutoRenew function can be directly deployed to a user's Azure Account from the [GitHub](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal) project page.

## RCL SSL HTTP AutoRenew

The [RCL SSL HTTP AutoRenew](./httpautorenew/httpautorenew.md) runs as a [Windows Service](./dnsautorenew/windows-service.md) in a Windows hosting machine and a [Linux Daemon](./dnsautorenew/linux-daemon.md) in a Linux hosting machine. The primary purpose of service is to automatically renew SSL/TLS certificates created in the [RCL SSL Portal](./portal/portal.md) using the [Stand Alone](./portal/stand-alone.md) (including [SAN](./portal/stand-alone-san.md)) option and save them to a folder in the hosting machine. The web server must be configured to use the certificates files from the folder. In this way, the installation and renewal of certificates in a web server (eg. Apache, Tomcat, NGINX, IIS, Express, etc) is fully automated.

## RCL SSL DNS AutoRenew

The [RCL SSL DNS AutoRenew](./dnsautorenew/dnsautorenew.md) runs as a [Windows Service](./dnsautorenew/windows-service.md) in a Windows hosting machine and a [Linux Daemon](./dnsautorenew/linux-daemon.md) in a Linux hosting machine. The primary purpose of RCL SSL AutoRenew is to automatically renew SSL/TLS certificates created in the [RCL SSL Portal](./portal/portal.md) using the [Azure DNS](./portal/azure-dns.md) (including [SAN](./portal/azure-dns-san.md)) option and save them to a folder in the hosting machine. The web server must be configured to use the certificates files from the folder. In this way, the installation and renewal of certificates in a web server (eg. Apache, Tomcat, NGINX, IIS, Express, etc) is fully automated.

## RCL SSL DNS AutoRenew for Docker

[RCL SSL DNS AutoRenew for Docker](./containers/containers.md) is a docker image hosted on [Docker Hub](https://hub.docker.com/r/rclssl/dns-autorenew). You can use RCL SSL DNS AutoRenew for Docker to automatically install and renew SSL/TLS certificates in a docker host created in the RCL SSL Portal using the the following creation option:

- [Azure DNS](./portal/azure-dns.md) (including [SAN](./portal/azure-dns-san.md))

Certificates will be saved to a volume on the host machine for an ingress controller to use. RCL SSL DNS AutoRenew for Docker can be used to provide SSL/TLS certificates for :

- [Docker Deployments](./containers/docker.md)
- [Azure Container Instance](./containers/aci.md)
- [NGINX Ingress Controller](./containers//nginx.md)




