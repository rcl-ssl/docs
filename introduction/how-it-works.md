---
title: How it Works
description: Overview of RCL SSL certificate order, domain validation , certificate creation and installation
parent: Introduction
nav_order: 1
---

# Overview
**V7.1.0**

RCL SSL creates SSL/TLS certificates using the [Let's Encrypt V2 API](https://letsencrypt.org/). Certificates are created in a simple-to-use Web UI called the [RCL SSL Portal](/portal/portal.md). You can create up to 50 certificates using the RCL SSL Portal for a single subscription. If you need additional certificates you can create other subscriptions. Each subscription must be assigned to a unique email address / user account.

![image](/images/portal/portal.PNG)

# Order a Certificate

You will create an order for a certificate for your domain. A certificate order can be for a single domain (eg. acme.com), a www domain (eg. www.acme.com), a subdomain (eg. store.acme.com). An order can also include two domains in a single certificate, eg. www.acme.com and acme.com ; or *.acme.com and acme.com. This is known as a Subject Alternative Name (SAN) certificate. A third type of certificate is the Wildcard certificate, eg. *.acme.com. This single certificate supports an unlimited number of subdomains.

# Validate your Domain
Before a certificate can be created, the certificate order must be validated. To validate an order, you will need to prove that you own or have control over your domain. A challenge must be completed to prove that you control the domain. There are two types of challenges:

## HTTP Challenge

In the HTTP Challenge, you will need to add a file in the root folder of your website in a specific folder. You must have access to your website files in your hosting machine to add this file.

![image](../images/introduction/http-challenge1.png)

The file should be publicly accessible in a web browser.

![image](../images/portal/stand-alone-http-validation-test.PNG)

## DNS Challenge

In the DNS Challenge, you will need to add a DNS TXT Record with a specific value with your DNS provider. You must have access to manage the DNS Records for your domain with your domain provider.

![image](../images/portal/stand-alone-dns-record.PNG)

# Create a Certificate

Once your domain is validated, you will create your SSL/TLS certificate. The certificate will be stored in the Certificate's List in the RCL SSL portal. You can view and manage all your certificates in this list.

![image](../images/portal/certificate-details.png)

# Install a Certificate

Once the certificate is created, you can download the certificate files in the RCL SSL Portal to install in your web server.

![image](../images/portal/certificate-download.PNG)


![image](../images/portal/certificate-download-webserver.PNG)

You can then install the certificate files in your web server. The following links provides instructions on how to install the certificate in a web server

- [Installing SSL/TLS Certificates in Web Servers and Hosting Services](../installations/web-servers)
- [Installing SSL/TLS Certificates in Apache Server](../installations/apache)
- [Installing SSL/TLS Certificates in Apache Tomcat](../installations/apache-tomcat)
- [Installing SSL/TLS Certificates in NGINX](../installations/nginx)
- [Installing SSL/TLS Certificates in IIS](../installations/iis)

# Certificate Renewal

Certificates will expire in 90 days. You can delete the expired certificate, create a new certificate and install the new certificate in your web server. Alternatively, you can use one of the RCL SSL applications to automatically renew and install the certificates in your hosting machine. The following applications are available for automatic certificate renewal:

 - [RCL SSL HTTP AutoRenew](/httpautorenew/httpautorenew.md)
 - [RCL SSL CertificateBot](/certbot/certbot.md)
 - [RCL SSL AutoRenew Function](/autorenew/autorenew.md)

 # Hosting Machines

 RCL SSL supports certificate installation in Linux and Windows hosting machines. The hosting machines can be on-premise or in the cloud. Examples of cloud hosting machines include: Azure VM, AWS EC2, Google Cloud Compute. Single instance hosting machines are ideal, there is no need for load balancers or applications gateways to install the certificates. The certificates are installed directly in hosting machine.

 Virtual Private Server (VPS) hosting is also supported, in addition to, products like Linode and other similar web server hosting services.