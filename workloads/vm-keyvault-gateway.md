---
title: Azure Virtual Machine with Key Vault, DNS and Application Gateway
description: Automatically create, install and renew a SSL/TLS certificates in an Azure VM using Key Vault, DNS and Application Gateway
parent: Workloads
nav_order: 2
---

# Azure Virtual Machine with Key Vault, DNS and Application Gateway

**V6.0.10**

This workload allows for the **automatic creation, installation and renewal** of a SSL/TLS certificate for [Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/virtual-machines/) using :

- [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/certificates/about-certificates) 
- [Azure DNS](https://docs.microsoft.com/en-us/azure/dns/) 
- [Azure Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/overview)

# STEPS

## Step 1 : Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the :
    - [Azure DNS + Key Vault](../portal/azure-keyvault.md) option
    - [Azure DNS + Key Vault SAN](../portal/azure-keyvault-san.md) option

- The SAN option allow for two domains (wild card + naked domain, eg: *.contoso.com, contoso.com) on the certificate, whereas, the other option only allows one domain on the certificate.

## Step 2 : Certificate Automatically Imported to Key Vault

- After creation, the certificate is automatically imported to Azure Key Vault
- Check for the **certificate name** and version in Azure Key Vault

## Step 3 : TLS Termination with Azure Application Gateway

Application Gateway supports TLS termination at the gateway, after which traffic typically flows unencrypted to the backend servers or virtual machines.

- Learn about : [TLS Termination with Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/ssl-overview)
- Learn about : [Virtual Machines with Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/quick-create-portal)
- After creating and installing the SSL/TLS certificate in Azure Key Vault, follow the instructions in the link below to configure TLS termination with the Key Vault certificate and Application Gateway V2 :

- [Configure TLS termination with Key Vault certificates and Application Gateway V2](https://docs.microsoft.com/en-us/azure/application-gateway/configure-key-vault-portal)

## Step 4 : Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to automatically renew the certificate.

- Use the [RCL AutoRenew Function](../autorenew/introduction.md) to automatically renew certificates
- The certificates will be automatically renewed , imported to Key Vault and the TLS termination with Application gateway will be updated without any user interaction being required


