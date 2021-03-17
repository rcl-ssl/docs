---
title: Automatic Renewal
description: Automatic renewal of SSL/TLS certificates created in the RCL portal
parent: Portal
nav_order: 9
---

# Automatic Renewal of SSL/TLS Certificates

In this section, we will discuss the various options for the automatic renewal of certificates created in the RCL portal.

## RCL CertificateBot

If you are hosting your website in a Windows or Linux Server in a Virtual Machine or Container, [CertificateBot](../certbot/certbot) is the ideal option to automatically renew the SSL/TLS certificates.

It is recommended that you create certificates using the following options :

- [Azure DNS](../portal/azure-dns) or
- [Azure DNS - SAN](../portal/azure-dns-san)

Certificates created with an Azure DNS Zone qualifies for automatic renewals.

**Certificates created with [Stand Alone](../portal/stand-alone) or [Stand Alone - SAN](../portal/stand-alone-san) cannot be automatically renewed.**

If you are using CertificateBot, please **DO NOT use the AutoRenew Function**. CertificateBot will carry out the operations of the AutoRenew function and both should not be used together.

### Windows Server

CertificateBot runs as a [Windows Service](../certbot/windows-service) in a Windows Server. It saves SSL/TLS certificates from the RCL portal to a folder in the Windows Server. Every four days, it sends a request to renew SSL/TLS certificates. Certificates that are about to expire are automatically renewed and the certificate files are saved in the server to a specified folder.

#### Web Servers on Windows

The web servers in the Windows Server must be configured to use the SSL/TLS certificate files saved in the specified folder in the server. You can use the following guidance for installing SSL/TLS certificates in the following web servers :

- [Apache](../installations/apache)
- [Apache Tomcat](../installations/apache-tomcat)
- [NGINX](../installations/nginx)
- [Other Web Servers](../installations/web-servers)

#### Special Support for IIS

CertificateBot in a Windows Server has [Special Support for IIS](../certbot/iis). You can configure CertificateBot with the bindings of the websites hosted in IIS. Once the bindings are configured, CertificateBot will automatically install and renew SSL/TLS certificates for each of the websites' binding.

### Linux Server

CertificateBot runs as a [Linux Daemon](../certbot/linux-daemon) in a Linux Server. It saves SSL/TLS certificates from the RCL portal to a specified folder in the Linux Server. Every four days, it sends a request to renew SSL/TLS certificates. Certificates that are about to expire are automatically renewed and the certificate files are saved in the server.

#### Web Servers on Linux

The web servers must be configured to use the SSL/TLS certificate files saved in the specified folder in the server. You can use the following guidance for installing SSL/TLS certificates in the following web servers :

- [Apache](../installations/apache)
- [Apache Tomcat](../installations/apache-tomcat)
- [NGINX](../installations/nginx)
- [Other Web Servers and Hosting Services](../installations/web-servers)

## RCL AutoRenew Function

The [AutoRenew Function](../autorenew/autorenew) is the ideal choice for the automatic installation and renewal of certificates created for [Azure App Services](../portal/azure-appservice).

The AutoRenew function can also be used to automatically renew and install certificates for [Azure Key Vault](../portal/azure-keyvault) and [Azure Key Vault - SAN](../portal/azure-keyvault-san).

The AutoRenew Function is an Azure Function that runs on a Consumption plan.

The AutoRenew function will run every week, if it finds a certificate about to expire, it will automatically renew the certificate and bind it to the App Service or save it to Azure Key Vault. The older certificate is replaced with the newer one.

## RCL API and SDK

If you need to create a custom solution to renew SSL/TLS certificates in your server or system, you can use the RCL API or the RCL SDK.

### RCL API

The [RCL API](../api/api) is a REST API Service to get and renew SSL/TLS certificates in the RCL portal. You can explore the API in the [RCL API Developer's site](https://rclapi.developer.azure-api.net/).

### RCL SDK

The [RCL SDK](../sdk/sdk) is a C# library available on NuGet. You can use the SDK to make authorized requests to the RCL API. The SDK makes development easier and requires less lines of code than if you were using the RCL API directly. 