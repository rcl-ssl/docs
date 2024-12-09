---
title: Introduction
description: The RCL SSL client for Let's Encrypt allows you to create SSL/TLS certificates for your web sites / applications using the popular Let's Encrypt V2 API.
has_children: false
nav_order: 1
---

# Introduction
**V8.0**

The RCL SSL Client for *Let's Encrypt*<sup>TM</sup> allows you to create free SSL/TLS certificates for your web sites / applications using the popular *Let's Encrypt*<sup>TM</sup> V2 API.

![image](./images/portal/rcl_ssl_200.png)

Use the RCL SSL Portal to  create and renew single or multiple-domain SSL/TLS certificates for your web sites / applications. The following domains are supported

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

- Automatically create and install SSL/TLS certificates in Microsoft Azure Services such as [Azure Virtual Machines](./workloads/vm.md), [Azure Key Vault](./workloads/keyvault.md), [Azure Application Gateway](./workloads/appgateway.md), [Azure App Services](./workloads/app-service.md) and [Azure Kubernetes Service](./workloads/aks.md).


# RCL SSL AutoRenew Function

The [RCL SSL AutoRenew](/autorenew/autorenew) function is an Azure Function app that runs in an [Azure Consumption Plan](https://docs.microsoft.com/en-us/azure/azure-functions/consumption-plan). The primary purpose of the RCL SSL AutoRenew Function is to automate the renewal and installation of certificates created in the [RCL SSL Portal](./portal/portal.md) for an [Azure App Service](./portal/azure-appservice.md) or [Azure Key Vault](./portal/azure-keyvault.md) . The RCL SSL AutoRenew function can be directly deployed to a user's Azure Account from the [GitHub](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal) project page.

# RCL SSL API

The [RCL SSL API](./api/api.md) is used to programmatically create and renew certificates created in the **RCL SSL Portal**. 

# RCL SSL SDK

The [RCL SSL SDK](./sdk/sdk.md) provides a C# .NET Core library to make authorized requests to the [RCL SSL API](../api/api.md). Use the SDK to get, create and renew SSL/TLS certificates in a user's subscription in the [RCL Portal](../portal/portal.md).











