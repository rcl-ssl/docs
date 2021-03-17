---
title: Web Servers
description: Using RCL to install SSL/TLS certificates in Web Servers or web hosting systems.
parent: Certificate Installations
nav_order: 5
---

# Installing SSL/TLS Certificates in Web Servers

In this section, we will discuss a general approach to installing SSL/TLS certificates in web servers or web hosting systems.

## General Approach

The general approach to installing SSL/TLS in a web server or hosting system is to :

- Download the SSL/TLS certificate files from the certificate provider
- Save the certificate files to a folder in your system
- Configure the web server or hosting system to use the files to enable SSL for your website

## SSL/TLS Certificate Files

Web Servers or Hosting Systems may need one or more of the following certificate files :

- **Certificate Private Key** (.key) : this is the private key for the certificate. This file usually uses the '.key' extension, but could be opened as a text file.

- **Primary Certificate** (.crt) : this is the primary certificate for your domain. It does not contain the private key. This file usually uses the '.crt' extension, but could be opened as a text file.

- **Intermediate Certificate (or Certificate Authority (CA) Bundle)** (.crt) - these are the intermediate certificates from the Certificate Authority (CA). The intermediate certificates are stored in a **single** file. It does not contain the private key. This file usually uses the '.crt' extension, but could be opened as a text file.

- **Full Chain Certificate** (.crt) - this is a single file that contains the primary certificate and all the intermediate certificates. It does not contain the private key. This file usually uses the '.crt' extension, but could be opened as a text file.

**All of the above certificate files are provided in the RCL portal in the 'Details' page for the Certificate.**

## Installing the Certificate Files

### Configuration File

Most web servers and hosting systems must be configured to install SSL/TLS in your website. This is done with a configuration file. In the configuration file , you will specify the file path where the certificate files are stored for each certificate file required by the server or system.

### Text 

Some systems may allow you to paste the required certificate files as text. You will need to open each file in a text editor, copy the text and paste it into the system

## Testing SSL/TLS

To test the SSL/TLS after installation, restart the web server or system and navigate to your web site. The browser will indicate if SSL is enabled for your website and whether the certificate is valid.