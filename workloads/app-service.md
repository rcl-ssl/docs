---
title: Azure App Service
description: Using RCL SSL to automatically create, install and renew a SSL/TLS certificates in an Azure App Service
parent: Workloads
nav_order: 4
---

# SSL/TLS for Azure App Service

**V8.0**

This workload allows for the **automatic creation, installation and renewal** of a SSL/TLS certificate in an [Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/) (Web App, Function App, API App, Mobile App, etc.). This workload also supports apps in slots.

# Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the:

    - [Azure App Service](../portal/azure-appservice.md) option
    - [Azure App Service SAN](../portal/azure-appservice-san.md) option

- The SAN options allow for two domains on a single certificate, whereas, the other option only allows one domain on the certificate

# Certificate Automatically Bound to the App Service

- After creation, the certificate is automatically installed in the App Service Plan and bound to the App Service

# Manually Renewing a SSL/TLS Certificate

- In the Certificate List, click on **Manage > Renew**
- Then renew the certificate

# Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to automatically renew the certificate.

- Use the [RCL SSL AutoRenew Function](../autorenew/introduction.md) to automatically renew certificates 
- The certificates will be automatically renewed , installed in the App Service Plan and bound to the App Service without any user interaction being required


