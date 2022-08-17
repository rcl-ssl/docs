---
title: RCL AutoRenew Function
description: Using the RCL AutoRenew Function to renew SSL/TLS certificates created in the RCL portal
has_children: true
nav_order: 5
---

# RCL AutoRenew Function
**V6.0.10**

The [RCL AutoRenew Function](../autorenew/autorenew.md) is a Microsoft Azure Function app that automatically renews SSL/TLS certificates created in the [RCL Portal](../portal/portal.md).

## Automatically Renew SSL/TLS Certificates

You can use the function app to automatically renew SSL/TLS certificates created in the [RCL Portal](../autorenew/autorenew.md) using the the following creation options :

- Azure Key Vault + DNS (including SAN)
- Azure DNS (including SAN)
- Azure App Services 

**'Stand Alone' certificates are not supported by the AutoRenew function.**

The RCL AutoRenew Function is ideally suited for renewal of certificates for **Key Vault** and **Azure App Services**. 

The function app will run once a week and automatically update certificates that are about to expire.