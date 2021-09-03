---
title: Introduction
description: The RCL client for Let's Encrypt allows you to create SSL/TLS certificates for your web sites / applications using the popular Let's Encrypt V2 API.
has_children: false
nav_order: 1
---

# Introduction

The RCL client for *Let's Encrypt*<sup>TM</sup> allows you to create SSL/TLS certificates for your web sites / applications using the popular *Let's Encrypt*<sup>TM</sup> V2 API.

<sub>Let's Encrypt is a trademark of the [Internet Security Research Group](https://www.abetterinternet.org/). All rights reserved.</sub>

Use the applications to create and renew single or multiple-domain SSL/TLS certificates for your web sites / applications. The following domains are supported

- Naked apex domains (e.g. contoso.com)
- Sub-domains (e.g. store.contoso.com, www.contoso.com)
- Wild card domains (e.g. *.contoso.com) 
- SAN mutli-domains (multiple domains in a single certificate) 

# RCL Portal

The [RCL portal](../portal/portal) is the primary application. It is a SaaS application that you can [Subscribe](../subscription/subscription) for.

![image](./images/portal/portal.PNG)

The RCL portal is a simple-to-use online Web UI and allows you to :

## Common Features

- Create [Single](../portal/stand-alone) and [Multi-Domain SAN](../portal/stand-alone-san) SSL/TLS certificates manually. You can download the certificates and manually install them in your web servers. It is ideal for web applications hosted in a Hosting Provider, Virtual Machine or Container where manual installation and renewal of SSL/TLS certificates in web servers (eg. Apache, Tomcat, NGINX, IIS, Express, etc.) do not prove to be a problem.

## Microsoft Azure Integrated Services

- Create [Single](../portal/azure-dns) and [Multi-Domain SAN](../portal/azure-dns-san) SSL/TLS certificates automatically using an [Azure DNS Zone](https://docs.microsoft.com/en-us/azure/dns/dns-zones-records). This option allows you to automatically install and renew certificates in a Windows or Linux server (VM or Container) using [RCL CertificateBot](../certbot/certbot). Many popular web servers are supported, eg. Apache, Tomcat, NGINX, IIS, Express, etc.

- Create a [Single Domain](../portal/azure-appservice) SSL/TLS certificate for an **Azure App Service** (Web App, Mobile App, Function App). The certificate is automatically created and bound to the App Service. You can use the [RCL AutoRenew Function app](../autorenew/autorenew) to automatically renew and bind the SSL/TLS certificate in the App Service.

- Create [Single](../portal/azure-keyvault) and [Multi-Domain SAN ](../portal/azure-keyvault-san) SSL/TLS certificates using an [Azure DNS Zone](https://docs.microsoft.com/en-us/azure/dns/dns-zones-records) and automatically save the certificate to [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/general/basic-concepts). You can use the SSL/TLS certificate from Key Vault in other services. The certificate can be automatically renewed and saved to Key vault using the [RCL AutoRenew Function app](/autorenew/autorenew).

# The Other RCL Apps

## Azure Integrated Services

### RCL CertificateBot

The [RCL CertificateBot](../certbot/certbot) runs as a [Windows Service](../certbot/windows-service) in a Windows Server and a [Linux Daemon](../certbot/linux-daemon) in a Linux Server. The primary purpose of CertificateBot is to automatically renew SSL/TLS certificates created in the RCL portal and save them to a folder in the server (VM or Container). The web server must be configured to use the certificates files from the folder. In this way, the [Installation and Renewal](../installations/installations) of certificates in a web server (eg. Apache, Tomcat, NGINX, IIS, Express, etc) is fully automated. 

CertificateBot also provides [Special Support for IIS](../certbot/iis), it allows for the automatic renewal and binding of SSL/TLS certificates to websites hosted in IIS. CertificateBot is an open-source project and is available on [GitHub](https://github.com/rcl-ssl/RCL.CertificateBot).

### RCL AutoRenew Function

The [RCL AutoRenew](/autorenew/autorenew) function is an Azure Function app that runs in a [Consumption Plan](https://docs.microsoft.com/en-us/azure/azure-functions/consumption-plan). The primary purpose of the AutoRenew Function is to automate the renewal and installation of certificates created in the RCL portal for an **Azure App Service** or **Azure Key Vault**. The AutoRenew function is an open-source project and can be directly deployed to a user's Azure Account from the [GitHub](https://github.com/rcl-ssl/RCL.AutoRenew) project page.

# REST API and SDK

## RCL API

The [RCL API](../api/api) is a REST API service to get and renew SSL/TLS certificates created in the RCL portal. You can explore the API on the [RCL API Developer's Page](https://rclapi.developer.azure-api.net/). You can use the API to create your own applications to automate the installation and renewal of SSL/TLS certificates created in the RCL Portal for use in web servers (eg. Apache, Tomcat, NGINX, IIS, Express, etc.) in a Windows or Linux Server (VM or Container).

## RCL SDK

The [RCL SDK](../sdk/sdk) is a C# Library that facilitates making authenticated requests to the RCL API. You can use the SDK to build applications to automate the installation and renewal of SSL/TLS certificates created in the RCL Portal for use in web servers (eg. Apache, Tomcat, NGINX, IIS, Express, etc.) in a Windows or Linux Server (VM or Container). You can include the SDK in your .NET projects from NuGet (search for RCL.SDK). The RCL SDK is an open-source project available on [GitHub](https://github.com/rcl-ssl/RCL.SDK).

