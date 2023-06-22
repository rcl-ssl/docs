---
title: Introduction
description: The RCL client for Let's Encrypt allows you to create SSL/TLS certificates for your web sites / applications using the popular Let's Encrypt V2 API.
has_children: false
nav_order: 1
---

# Introduction
**V7.0.0**

The RCL client for *Let's Encrypt*<sup>TM</sup> allows you to create SSL/TLS certificates for your web sites / applications using the popular *Let's Encrypt*<sup>TM</sup> V2 API.

<sub>Let's Encrypt is a trademark of the [Internet Security Research Group](https://www.abetterinternet.org/). All rights reserved.</sub>

Use the various RCL SSL Apps to create and renew single or multiple-domain SSL/TLS certificates for your web sites / applications. The following domains are supported

- Naked apex domains (e.g. contoso.com)
- Sub-domains (e.g. store.contoso.com, www.contoso.com)
- Wild card domains (e.g. *.contoso.com) 
- SAN mutli-domains (multiple domains in a single certificate) 

# RCL SSL Portal

The [RCL SSL portal](../portal/portal) is the **primary application**. It is a SaaS application that you can [Subscribe](../subscription/subscription) for in the [Azure Market Place](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/rayconsulting.002?tab=Overview).

![image](./images/portal/portal.PNG)

The RCL SSL portal is a simple-to-use online Web UI and allows you to :

## Basic Features

- Create [Single](../portal/stand-alone) and [Multi-Domain SAN](../portal/stand-alone-san) SSL/TLS certificates manually. You can download the certificates and manually install them in your web servers. It is ideal for web applications hosted in a Hosting Provider or Virtual Machine where manual installation and renewal of SSL/TLS certificates in web servers (eg. Apache, Tomcat, NGINX, IIS, Express, etc.) do not prove to be a problem.

## Microsoft Azure Integrated Services

- Create [Single](../portal/azure-dns) and [Multi-Domain SAN](../portal/azure-dns-san) SSL/TLS certificates automatically using an [Azure DNS Zone](https://docs.microsoft.com/en-us/azure/dns/dns-zones-records). 

- Create a [Single Domain](../portal/azure-appservice) SSL/TLS certificate for an **Azure App Service** (Web App, Mobile App, Function App). The certificate is automatically created and bound to the App Service. You can use the [RCL SSL AutoRenew Function app](../autorenew/autorenew) to automatically renew and bind the SSL/TLS certificate in the App Service. Web Apps in slots are supported.

- Create [Single](../portal/azure-keyvault) and [Multi-Domain SAN ](../portal/azure-keyvault-san) SSL/TLS certificates using an [Azure DNS Zone](https://docs.microsoft.com/en-us/azure/dns/dns-zones-records) and automatically save the certificate to [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/basic-concepts). You can use the SSL/TLS certificate from Key Vault in other services (eg: Azure Application Gateway and Azure Kubernetes Service). The certificate can be automatically renewed and saved to Key vault using the [RCL SSL AutoRenew Function app](/autorenew/autorenew).

# The Other RCL Apps

## RCL SSL CertificateBot

The [RCL SSL CertificateBot](../certbot/certbot) runs as a [Windows Service](../certbot/windows-service) in a Windows hosting machine and a [Linux Daemon](../certbot/linux-daemon) in a Linux hosting. The primary purpose of CertificateBot is to automatically renew SSL/TLS certificates created in the RCL portal using the Azure DNS (including SAN) option and save them to a folder in the hosting machine (Virtual Machine). The web server must be configured to use the certificates files from the folder. In this way, the [Installation and Renewal](../installations/installations) of certificates in a web server (eg. Apache, Tomcat, NGINX, IIS, Express, etc) is fully automated. RCL SSL CertificateBot is an open-source project and is available on [GitHub](https://github.com/rcl-ssl/RCL.SSL.CertificateBot).

## RCL SSL CertificateBot for IIS

RCL SSL CertificateBot also provides [Special Support for IIS](../certbot/iis), it allows for the automatic renewal and binding of SSL/TLS certificates to websites hosted in IIS. RCL SSL CertificateBot for IIS is an open-source project and is available on [GitHub](https://github.com/rcl-ssl/RCL.SSL.CertificateBot).

## RCL SSL AutoRenew Function

The [RCL SSL AutoRenew](/autorenew/autorenew) function is an Azure Function app that runs in a [Consumption Plan](https://docs.microsoft.com/en-us/azure/azure-functions/consumption-plan). The primary purpose of the RCL SSL AutoRenew Function is to automate the renewal and installation of certificates created in the RCL SSL Portal for an **Azure App Service** , **Azure Key Vault** or **Azure DNS**. The RCL SSL AutoRenew function is an open-source project and can be directly deployed to a user's Azure Account from the [GitHub](https://github.com/rcl-ssl/RCL.SSL.AutoRenew.Function) project page.

# REST API 

## RCL SSL API

The [RCL SSL API](../api/api) is a REST API service to get and renew SSL/TLS certificates created in the [RCL SSL Portal](./portal/portal.md). It is primarily focused on automating the renewal of certificates. It applies to certificates created with the following options :

- [Azure DNS](./portal/azure-dns.md) (Including [SAN](./portal/azure-dns-san.md))
- [Azure DNS + Key Vault](./portal/azure-keyvault.md) (Including [SAN](./portal/azure-keyvault-san.md))
- [Azure App Service](./portal/azure-appservice.md)

You can use the API to create your own applications to automate the installation and renewal of SSL/TLS certificates created in the RCL SSL Portal.



