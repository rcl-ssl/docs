---
title: Azure Virtual Machine
description: Using RCL SSL to automatically create, install and renew a SSL/TLS certificates in an Azure Virtual Machine
parent: Workloads
nav_order: 1
---

# SSL/TLS for Azure Virtual Machines 
**V8.0**

This workload is applicable for the **creation, installation and renewal** of a SSL/TLS certificate in Azure Virtual Machines (VM) (Linux or Windows) running a web server.

The web servers running in the VM may include : 

 - Apache
 - Apache Tomcat
 - Nginx
 - Microsoft IIS
 - Other web servers and hosting systems

# Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL SSL Portal by using any of the following options :

    - [Stand Alone](../portal/stand-alone.md) 
    - [Stand Alone SAN](../portal/stand-alone-san.md) 
    - [Azure DNS](../portal/azure-dns.md)
    - [Azure DNS SAN](../portal/azure-dns-san.md)

- The SAN options allow for two domains on a single certificate, whereas, the other option only allows one domain on the certificate

# Install the SSL/TLS Certificate in a Web Server

- Install the SSL/TLS Certificate in a web server running in the VM :

    - [Apache](../installations/apache.md)
    - [Apache Tomcat](../installations/apache-tomcat.md)
    - [NGINX](../installations/nginx.md)
    - [Microsoft IIS](../installations/iis.md)
    - [Other web servers and hosting systems](../installations/web-servers.md)

# Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to renew the certificate.

## Manual Renewal - Stand Alone and Stand Alone SAN

- Delete the SSL/TLS certificate in the RCL SSL Portal just before it expires
- Create a new certificate using the 'Stand Alone' or 'Stand Alone SAN' option
- Remove the old certificate and re-install the new one in your web server

## Manual Renewal - Azure DNS and Azure DNS SAN

- In the Certificate List, click on **Manage > Update**
- Then update the certificate
- Remove the old certificate and re-install the new one in your web server

## Automatic Renewal - Azure DNS + Key Vault (including SAN) + Application Gateway

### Create the SSL/TLS Certificate

- Create the SSL/TLS certificate in the RCL SSL Portal by using either the :
    - [Azure DNS + Key Vault](../portal/azure-keyvault.md) option
    - [Azure DNS + Key Vault SAN](../portal/azure-keyvault-san.md) option

- The SAN option allow for two domains (wild card + naked domain, eg: *.contoso.com, contoso.com) on the certificate, whereas, the other option only allows one domain on the certificate.

### Certificate Automatically Imported to Key Vault

- After creation, the certificate is automatically imported to Azure Key Vault
- Check for the **certificate name** and version in Azure Key Vault

### Azure Application Gateway SSL/TLS with Azure Key Vault

Application Gateway supports TLS termination at the gateway, after which traffic typically flows unencrypted to the backend servers or virtual machines. Follow the instruction in this link to add the SSL/TLS certificate for Azure Key Vault and VMs

- [Create an Application Gateway V2 and attach Virtual Machines](https://learn.microsoft.com/en-us/azure/application-gateway/quick-create-portal)

- [Configure TLS termination with Key Vault certificates and Application Gateway V2](https://docs.microsoft.com/en-us/azure/application-gateway/configure-key-vault-portal)

### Automatically Renewing a SSL/TLS Certificate

SSL/TLS Certificates will expire within 90 days. Follow these instructions to automatically renew the certificate.

- Use the [RCL SSL AutoRenew Function](../autorenew/introduction.md) to automatically renew certificates
- The certificates will be automatically renewed , imported to Key Vault and the TLS termination with Application gateway will be updated without any user interaction being required


