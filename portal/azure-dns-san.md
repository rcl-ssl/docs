---
title: Azure DNS SAN
description: Use the RCL portal to create Multi-Domain SAN SSL/TLS certificates using an Azure DNS Zone 
parent: Portal
nav_order: 5
---

# SAN Certificates - Azure DNS

A Subject Alternative Name (SAN) TLS/SSL certificate will contain multiple domains in a single certificate. SAN certificates created with an Azure DNS Zone will contain the naked apex domain (e.g. contoso.com) and the wild card domain (e.g. *.contoso.com) in a single TLS/SSL certificate.

# Single Apex Domains

SAN certificates only allow a single apex domain. For instance the two domains 'fabricam.com' and 'contoso.com' are not allowed in a SAN multi-domain certificate.

# Access Control

## AAD Accounts

**Personal and Microsoft Accounts are not supported for Azure DNS. Only Azure Active Directory (AAD) organizational accounts (also known as ‘Work or School Accounts’) are supported.**

If you try to manage an Azure DNS with a MSA account you will get the following error.

![image](../images/portal/arm-consent-error.PNG)

If you signed up for RCL with a personal Microsoft account (MSA), please follow the instructions in the following link to associate an AAD account to your subscription:

- [Sign-In Accounts for RCL Lets](../authorization/sign-in-accounts)

## Set Access Control

To create certificates for Azure DNS, the Azure AAD organizational account that you use to login to RCL must either be :

- An administrator to the subscription containing the Azure DNS Zone(s)

- Have a role of ‘Owner’ or ‘Contributor’ to the subscription containing the Azure DNS Zone(s)

If either of these requirements are not met, the ‘subscriptions’ and ‘DNS Zone’ lists will be empty when you try to create a certificate.

![image](../images/portal/access-control-subscriptions_dns_empty.png)

You may also experience an error message.

![image](../images/portal/access-control-errormsg.png)

To set up access control for your AAD account, follow the instructions in the link below :

- [Set Access Control for the AAD user](../authorization/access-control-user)

# Create a SAN TLS/SSL Certificate using DNS-01

RCL uses the DNS-01 challenge type to issue SAN certificates for :

- naked apex domain (e.g. contoso.com)
- wild card domain (e.g. *.contoso.com)
- both domains are included in a single TLS/SSL certificate

# Create a DNS Zone and Configure Name Server

If you bought your domain with a domain registrar, you must set up your Azure DNS Zone to manage the records for your domain.

![image](../images/portal/dns-zone-setup.png)

Follow the instructions in the link below to set up your DNS Zone and delegate the name server (NS) records for your domain :

- [Delegate DNS Zone](https://docs.microsoft.com/bs-latn-ba/azure/dns/dns-delegate-domain-azure-dns)

# Create SSL/TLS Certificate

- In the ‘Certificates’ module of the portal, click on the **Create New SSL/TLS Certificate** link

![image](../images/portal/create-new.PNG)

- Select the ‘Azure DNS SAN’ option.

![image](../images/portal/azure-dns-san-select.png)

- Add the data to create the certificate. The image below illustrates sample data.

![image](../images/portal/azure-dns-san-create.png)

- The Hostname is the single Apex Domain (eg: 'contoso.com') you are requesting the certificate for. Only a single domain is allowed. The additional wildcard domain (eg: *.contoso.com) will be automatically added to the certificate.

- In the case above, we are requesting a SAN SSL/TLS certificate for the naked apex domain, ‘shopeneur.com’. The wild card domain '*.shopeneur.com' will be automatically included in the certificate.

- The Host Name must be valid for the DNS Zone. For instance, the naked apex domain ‘shopeneur.com’ is valid for the DNS Zone ‘shopeneur.com’.

- You will need to wait up to 10 mins to validate the site and install the certificate. When this is done, the SSL/TLS certificate will be displayed in the certificates list.

![image](../images/portal/certificate-ordered.PNG)

- When this is done, the SSL/TLS certificate will be displayed in the certificates list.

![image](../images/portal/certificate-list.PNG)

# Manually Installing TLS/SSL Certificates in Web Servers

- To access the certificate, click the **Details** button in the certificates list page.

- You can download the certificate in .PFX, .CER, .CRT or .PEM formats.

![image](../images/portal/certificate-download.PNG)

- You can also download the Certificate files required for installation in specific web servers (Apache, Apache Tomcat, NGINX, etc). The files include :

- Certificate Private Key (.key)
- Primary Certificate (.crt)
- Intermediate Certificate (CA Bundle) (.crt)
- Full Chain Certificate (.crt)

![image](../images/portal/certificate-download-webserver.PNG)

## Certificate Installation

You will need to manually download and install your certificate in your web server. The following links provides instructions on how to install the certificate in a web server

- [Installing SSL/TLS Certificates in Web Servers and Hosting Services](../installations/web-servers)
- [Installing SSL/TLS Certificates in Apache Server](../installations/apache)
- [Installing SSL/TLS Certificates in Apache Tomcat](../installations/apache-tomcat)
- [Installing SSL/TLS Certificates in NGINX](../installations/nginx)
- [Installing SSL/TLS Certificates in IIS](../installations/iis)

# Manually Renewing SSL/TLS Certificates

SSL/TLS certificates will expire in 90 days. You can manually renew a certificate at any point before the expiry date. Click on the 'Update' link in the certificates list to update a certificate.

![image](../images/portal/azure-dns-update.PNG)

# Automatic Certificate Renewal and Installation

You can use the [RCL CertificateBot](../certbot/certbot) to automatically renew certificates and install them in web servers (Apache, Apache Tomcat, NGINX, IIS).

RCL CertificateBot can be installed in :

- Windows
- Linux

Follow the instructions in these links to use RCL CertificateBot :

- [RCL CertificateBot](../certbot/certbot)


# Rate Limits

**There is a rate limit of 50 SSL/TLS certificates per subscription.**

In addition, Let's Encrypt has instituted rate limits to ensure fair usage by as many people as possible. To find out more about these rate limits please refer to the following link :

- [Let's Encrypt Rate Limits](https://letsencrypt.org/docs/rate-limits/)