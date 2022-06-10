---
title: Azure Kubernetes Service with Key Vault and akv2k8s
description: Automatically create, install and renew a SSL/TLS certificates in an Azure Kubernetes Service
parent: Workloads
nav_order: 6
---

# Azure Kubernetes Service (AKS) with Key Vault and akv2k8s

**V6.0.10**

This workload allows for the **automatic creation, installation and renewal** of a SSL/TLS certificate for [Azure Kubernetes Service](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) using :

- [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/certificates/about-certificates) 
- [akv2k8s.io](https://akv2k8s.io/)

# STEPS

## Step 1 : Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL Portal by using either the :
    - [Azure DNS + Key Vault](../portal/azure-keyvault.md) option
    - [Azure DNS + Key Vault SAN](../portal/azure-keyvault-san.md) option

- The SAN option allow for two domains (wild card + naked domain, eg: *.contoso.com, contoso.com) on the certificate, whereas, the other option only allows one domain on the certificate.

## Step 2 : Certificate Automatically Imported to Key Vault

- After creation, the certificate is automatically imported to Azure Key Vault
- Check for the **certificate name** and version in Azure Key Vault

## Step 3 : Using akv2k8s for user secrets in AKS

Azure Key Vault to Kubernetes (akv2k8s) makes Azure Key Vault secrets, certificates and keys available in Kubernetes in a simple and secure way.

- Learn about : [akv2k8s](https://akv2k8s.io/)

- After creating and installing the SSL/TLS certificate in Azure Key Vault using the RCL portal, follow the instructions in the video link below to configure the certificate in a ingress controller in AKS using akv2k8s :

- [Certificates with Azure Key Vault and Nginx Ingress Controller](https://www.youtube.com/watch?v=qezjiilv9BM)

## Step 4 : Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to automatically renew the certificate.

- Use the [RCL AutoRenew Function](../autorenew/introduction.md) to automatically renew certificates
- The certificates will be automatically renewed , imported to Key Vault and the ingress controller and akv2k8s will ensure the certificate is updated in AKS without any user interaction being required


