---
title: Azure Key Vault
description: Using RCL SSL to automatically create, install and renew a SSL/TLS certificates in an Azure Key Vault
parent: Workloads
nav_order: 7
---

# SSL/TLS for Azure Key Vault

**V7.1.0**

This workload allows for the **automatic creation, installation and renewal** of a SSL/TLS certificate in an [Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/general/).

# Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the:

    - [Azure DNS + Key Vault](../portal/azure-keyvault.md) option
    - [Azure DNS + Key Vault](../portal/azure-keyvault-san.md) option

# Certificate Automatically added to Key Vault

- After creation, the certificate is automatically added to the Azure Key Vault certificate collection
 
# Manually Renewing a SSL/TLS Certificate

- In the Certificate List, click on **Manage > Update**
- Then update the certificate

# Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to automatically renew the certificate.

- Use the [RCL SSL AutoRenew Function](../autorenew/introduction.md) to automatically renew certificates 
- The certificates will be automatically renewed and added to Azure Key Vault without any user interaction being required