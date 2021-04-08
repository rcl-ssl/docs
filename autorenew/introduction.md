---
title: Introducing the Function
description: Using the RCL AutoRenew Function to renew SSL/TLS certificates created in the RCL portal
parent: AutoRenew Function
nav_order: 1
---

# Introduction

The **RCL AutoRenew Function** is a Microsoft Azure Function app that automatically renews SSL/TLS certificates created in the **RCL Portal**.

## Automatically Renew SSL/TLS Certificates

You can use the function app to automatically renew SSL/TLS certificates created in the **RCL Portal** using the the following creation options :

- **Azure App Services** 
- Azure Key Vault (including SAN)
- Azure DNS (including SAN)

**'Stand Alone' certificates are not supported by the Auto Renew function.**

The RCL AutoRenew Function is ideally suited for renewal of certificates for **Azure App Services** and **Key Vault**. 

If you need to automate the renewal and installation of certificates in your own webserver (Apache, Apache Tomcat, NGINX, IIS, etc) especially in a VM, please use the [RCL CertificateBot](../certbot/certbot) instead.

The function app will run once a week and automatically update certificates that are about to expire.

## Quick Start

Follow these steps to use the RCL AutoRenew Function :

- [Install the Function App in an Azure Account](./installation)
- [Configure the Function App](./configure)
- [Manually Test the Function App](./test)
