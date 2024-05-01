---
title: Virtual Machine Scale Sets
description: Using RCL SSL to automatically create, install and renew a SSL/TLS certificates in an Azure Virtual Machine Scale Set
parent: Workloads
nav_order: 2
---

# SSL/TLS for Azure Virtual Machine Scale Sets

**V7.1.0**

This workload allows for the **automatic creation, installation and renewal** of a SSL/TLS certificate for [Azure Virtual Machine Scale Sets](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview) using :

- [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/certificates/about-certificates) 
- [Azure DNS](https://docs.microsoft.com/en-us/azure/dns/) 
- [Azure Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/overview)

# Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL SSL Portal by using either the :
    - [Azure DNS + Key Vault](../portal/azure-keyvault.md) option
    - [Azure DNS + Key Vault SAN](../portal/azure-keyvault-san.md) option

- The SAN option allow for two domains (wild card + naked domain, eg: *.contoso.com, contoso.com) on the certificate, whereas, the other option only allows one domain on the certificate.

# Certificate Automatically Imported to Key Vault

- After creation, the certificate is automatically imported to Azure Key Vault
- Check for the **certificate name** and version in Azure Key Vault

# Add an Application Gateway to the VMSS

- Learn about : [Adding a Virtual Machine Scale Set to an Application Gateway](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking?tabs=portal1#add-a-virtual-machine-scale-set-to-an-application-gateway)

# Azure Application Gateway SSL/TLS with Azure Key Vault

Application Gateway supports TLS termination at the gateway, after which traffic typically flows unencrypted to the backend servers or virtual machines. Follow the instruction in this link to add the SSL/TLS certificate for Azure Key Vault

- [Configure TLS termination with Key Vault certificates and Application Gateway V2](https://docs.microsoft.com/en-us/azure/application-gateway/configure-key-vault-portal)

# Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to automatically renew the certificate.

- Use the [RCL SSL AutoRenew Function](../autorenew/introduction.md) to automatically renew certificates
- The certificates will be automatically renewed , imported to Key Vault and the TLS termination with Application gateway will be updated without any user interaction being required

# End-To-End SSL/TLS Encryption

If you require the connection from APplication Gateway to the individual VMs to use SSL/TLS on port 443, you will need to install SSL/TLS certificates in the VM. 

## Installing SSL/TLS in each VM

You can follow the instructions in this link to install SSL/TLS certificates in each VM

- [SSL/TLS for Azure Virtual Machines](./vm.md)

## Creating a Custom VM Image with RCL SSL

You can also create a custom VM image to use for your VM Scale Set the include one of RCL SSL Apps to automatically install and renew the certificate in the VM. You can install the following RCL apps in the custom VM image :

- [RCL SSL HTTP AutoRenew](../httpautorenew/)
- [RCL SSL DNS AutoRenew](../dnsautorenew/)


