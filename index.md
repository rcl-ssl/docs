---
title: Introduction
has_children: false
nav_order: 1
---

# Introduction

The RCL *Let's Encrypt*<sup>TM</sup> client allows you to Create TLS/SSL certificates for your web applications using the popular *Let's Encrypt*<sup>TM</sup> V2 API.

<sub>Let's Encrypt is a trademark of the Internet Security Research Group. All rights reserved.</sub>

This application is available as a SaaS offer in the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/rayconsulting.002?tab=overview).

Use the applications to create and renew single or multiple-domain TLS/SSL certificates for your web applications. Naked apex domains (e.g. contoso.com), sub-domains (e.g. store.contoso.com) and wild card domains (e.g. *.contoso.com) are all supported. 

## Features

- Supports HTTP-01 and DNS-01 challenge types

- Supports wild card domains (*.mysite.com) and naked apex domains (mysite.com)

- Supports SAN multi-domain certificates (mysite.com, www.mysite.com, *.mysite.com) all in a single certificate

- Create and download Stand Alone certificates to use for web apps in Virtual Machines or Containers

- Automatically install certificates in Azure App Services or Azure Key Vault 

- Easily subscribe to RCL Portal from the Azure Marketplace and start creating your certificates immediately.

## TLS/SSL Certificate Creation Options

You can create certificates using the following methods in the [RCL Portal](../portal/portal) :

**Stand Alone**

Manually create a single-domain or multi-domain (SAN*) TLS/SSL certificate. Certificates are downloadable.

**Azure DNS**

Create a single-domain or multi-domain (SAN*) TLS/SSL certificate automatically using an Azure DNS Zone. The certificate is downloadable and qualify for automatic renewals.

**Azure App Service**

Create a single-domain TLS/SSL certificate for an Azure App Service. It will be installed and bound to the App Service automatically. The certificate qualifies for automatic renewals.

**Azure Key Vault**

Create a single-domain or multi-domain (SAN*) TLS/SSL certificate using an Azure DNS Zone and save it to Azure Key Vault automatically. It can be used by other Azure Services from the Key Vault. The certificate qualifies for automatic renewals.

## Automatic Renewal

Use the free [RCL AutoRenew](/autorenew/autorenew) function app to automatically renew certificates created for Azure App Services, Azure DNS and Azure Key Vault.

## API

Get your certificates in the RCL Portal using the REST APIs. Use the [RCL API](../api/api) build your own automation system for certificate installation and renewal in your web server.

## Automation Services

Use the [RCL CertificateBot](../certbot/certbot) to automatically install and renew certificates in a Windows or Linux server. Use the certificate in Apache, Apache Tomcat, NGINX and Windows IIS.
