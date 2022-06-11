---
title: Web Servers
description: Using RCL to install SSL/TLS certificates in Web Servers or web hosting systems.
parent: Certificate Installations
nav_order: 1
---

# Installing SSL/TLS Certificates in Web Servers and Hosting Systems
**V6.0.10**

In this section, we will discuss a general approach to installing SSL/TLS certificates in web servers or web hosting systems. This is applicable if you host your website in a web server in a Windows or Linux Server (Virtual Machine). This may also be applicable if you host your website with a hosting provider or system.

## General Approach

The general approach to installing a SSL/TLS certificate in a web server or a hosting system is to :

- Download the SSL/TLS certificate files on your hosting machine
- Configure the web server or hosting system to use the files on the hosting machine to enable SSL for your website

## SSL/TLS Certificate Files

Web Servers or Hosting Systems may need one or more of the following certificate files :

- **Certificate Private Key** (.key) : this is the private key for the certificate. This file usually uses the '.key' extension, but could be opened as a text file or with a '.pem' extension.

- **Primary Certificate** (.crt) : this is the primary certificate for your domain. It does not contain the private key. This file usually uses the '.crt' or '.pem' extension, but could be opened as a text file.

- **Intermediate Certificate (or Certificate Authority (CA) Bundle)** (.crt) - these are the intermediate certificates from the Certificate Authority (CA). The intermediate certificates are stored in a **single** file. It does not contain the private key. This file usually uses the '.crt' or '.pem' extension, but could be opened as a text file.

- **Full Chain Certificate** (.crt) - this is a single file that contains the primary certificate and all the intermediate certificates. It does not contain the private key. This file usually uses the '.crt' or '.pem' extension, but could be opened as a text file.

- **PKCS#12** (.pfx or .p12) - this is a single file that contains the primary certificate and intermediate certificate files. It also contains the private key and may also be password protected. This is an archive file and uses the '.pfx' or '.p12' file extension.

**All of the above certificate files are provided in the RCL portal in the 'Details' page for the Certificate.**

## Installing the Certificate Files

### Configuration File

Most web servers and hosting systems must be configured to install SSL/TLS in your website. This is done with a configuration file. In the configuration file , you will specify the file path for each certificate file required by the server or system.

### Certificate Store
The .PFX certificate archive is usually 'extracted' and saved to a **Certificate Store** in your system. The certificate is then bound to your website by the webserver or hosting system using a configuration file or SSL binding system. Some web servers can use a .PFX file that is saved directly to the file system instead of a certificate store.

### Text 

Some systems may allow you to paste the required certificate files as text. You will need to open each file in a text editor, copy the text and paste it into the system

## Testing SSL/TLS

To test the SSL/TLS after installation, restart the web server or system and navigate to your web site. The browser will indicate if SSL is enabled for your website and whether the certificate is valid.