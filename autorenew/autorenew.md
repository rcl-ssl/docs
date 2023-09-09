---
title: AutoRenew Function
description: Using the RCL SSL AutoRenew Function to renew SSL/TLS certificates created in the RCL SSL portal
has_children: true
nav_order: 7
---

# RCL SSL AutoRenew Function
**V7.0.0**

The [RCL SSL AutoRenew Function](../autorenew/autorenew.md) is a Microsoft Azure Function app that automatically renews SSL/TLS certificates created in the [RCL SSL Portal](../portal/portal.md).

## Automatically Renew SSL/TLS Certificates

You can use the function app to automatically renew SSL/TLS certificates created in the [RCL SSL Portal](../autorenew/autorenew.md) using the the following creation options :

- [Azure Key Vault + DNS](../portal/azure-keyvault.md) (including [SAN](../portal/azure-keyvault-san.md))
- [Azure DNS](../portal/azure-dns.md) (including [SAN](../portal/azure-dns-san.md))
- [Azure App Services](../portal/azure-appservice.md) 

**'Stand Alone' certificates are not supported by the AutoRenew function.**

The function app will run once a week and automatically update certificates that are about to expire.