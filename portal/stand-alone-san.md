---
title: Stand Alone SAN
description: Use the RCL portal to manually create multi-domain SAN SSL/TLS certificates 
parent: Portal
nav_order: 3
---

# SAN Certificates - Stand Alone

A Subject Alternative Name (SAN) TLS/SSL certificate will contain multiple domains in a single certificate.

# HTTP SAN Certificate

A SAN certificate created with the HTTP Challenge will contain the naked apex domain (e.g. contoso.com) and the www subdomain (e.g. www.contoso.com) in a single TLS/SSL certificate.

# DNS SAN Certificate

A SAN certificate created with the DNS Challenge will contain the naked apex domain (e.g. contoso.com) and a wild card domain (e.g. *.contoso.com) in a single TLS/SSL certificate.

# Single Apex Domains

SAN certificates only allow a single apex domain. For instance the two domains 'fabricam.com' and 'contoso.com' are not allowed in a SAN multi-domain certificate.

# Creating Stand Alone SAN TLS/SSL Certificates

In the RCL Portal, you can create Stand Alone SAN TLS/SSL certificates using HTTP and DNS challenges. Your domain can be hosted with any domain registrar.

You will need to manually download and install the certificate in your web server.

You will need to manually download and install the certificate in your web server.

![image](../images/portal/flow-manual.png)

**When a certificate is close to expiration, you should delete the certificate and create a new one. Then, install the renewed certificate in your web server.**


You can create a TLS/SSL certificate by using either the :

- HTTP-01 Challenge or
- DNS-01 Challenge

## Create a SSL/TLS Certificate

- In the ‘Certificates’ module of the portal, click on the **Create New SSL/TLS Certificate** link

![image](../images/portal/create-new.PNG)

- Select the ‘Stand Alone SAN’ option.

![image](../images/portal/stand-alone-san-create.PNG)

# HTTP Challenge

RCL uses the HTTP-01 challenge type to create a certificate that includes the following domains in a single TLS/SSL certificate:

- naked apex domain (e.g. contoso.net)
- www subdomain (e.g. www.contoso.net)

To validate your domain with the HTTP challenge, you will be required to place files in the root of your website and ensure that these files can be accessed publicly on the web.

- Add the data to create the certificate. The image below illustrates data for a sample domain.

![image](../images/portal/stand-alone-san-http.PNG)

- The Hostname is the single Apex Domain (eg: 'contoso.com') you are requesting the certificate for. Only a single domain is allowed. The additional www subdomain will be automatically included in the certificate.

- In this case, we are requesting a SSL/TLS certificate for the naked apex domain, ‘shopeneur.com’. The www subdomain, 'www.shopeneur.com' will be automatically included in the certificate.

- Click the **Create** button when you are done
    
## Completing the HTTP Challenge

To validate your domain, you will be required to place two (2) files in the root of your website.

In your hosted website, you will need to create a folder named: .well-known/acme-challenge (note the dot at the start) in the root of your website.

Add a extension less file with the file name identified in the HTTP Validation page. To this file, add the content identified in the HTTP Validation page.

Ensure you can access the file publicly in the web browser by clicking on the link in the HTTP validation page. When you click on the link, you should see the validation content in the file displayed in the browser. If you do not see the content or the link is in-accessible the domain validation will fail.

![image](../images/portal/stand-alone-san-http-validation.PNG)

- The following example image illustrates the file in the web root directory

![image](../images/portal/stand-alone-san-http-token.PNG)

Perform the same steps for the second validation file.

![image](../images/portal/stand-alone-san-http-validation2.PNG)

**Note:** - for sites hosted in Azure App Service in a Windows Server, or the site is hosted in IIS, extension-less files are not served by default. To solve, this add the following ``web.config`` file to the ``acme-challenge`` folder.

```
<configuration>
    <system.webServer>
        <staticContent>
            <mimeMap fileExtension="." mimeType="text/plain"/>
        </staticContent>
    </system.webServer>
</configuration>
```

Click on the 'Validate' button when you are done.

# DNS Challenge

RCL uses the DNS-01 challenge to create a certificate that includes the following domains in a single TLS/SSL certificate:

- naked apex domain (e.g. contoso.net)
- wildcard (e.g. *.contoso.net)

To validate your domain with the DNS challenge, you will be required to create a DNS TXT record in your domain settings.

Add the data to create the certificate. The image below illustrates data for a sample domain.

![image](../images/portal/stand-alone-san-dns.PNG)

- The Hostname is the single Apex Domain (eg: 'contoso.com') you are requesting the certificate for. Only a single domain is allowed. The additional wildcard domain (eg: '*.contoso.com') will be automatically included in the certificate.

- In this case, we are requesting a SSL/TLS certificate for the naked apex domain, ‘shopeneur.com’. The wild card domain, '*.shopeneur.com', will be automatically included in the certificate.

## Completing the DNS Challenge

To validate the domain, you are required to create a DNS TXT record in your domain registrar or the application that manages your domain records.

In your management portal for your domain, add a DNS TXT record as defined in the ‘DNS Validation’ page (note the underscore '_').

Then add the two (2) separate values for the DNS TXT record as defined in the 'DNS Validation' page.

![image](../images/portal/stand-alone-san-dns-token.PNG)

The following is an example of the DNS TXT record.

![image](../images/portal/stand-alone-san-dns-record.PNG)

## Verifying the DNS TXT Record with Dig

- You can test the DNS record in the [Dig site](https://toolbox.googleapps.com/apps/dig/). In the site add the name identified in the DNS Validation page; and select the **TXT** record. The values for the record will be shown in the **;ANSWER** section

![image](../images/portal/dig-san.PNG)

- If you see the correct DNS TXT record and values, the test is successful

- If the test is successful, click the Validate button. 

# Certificate Creation

- You will need to wait up to 10 mins to validate the site and install the certificate. When this is done, the SSL/TLS certificate will be displayed in the certificates list.

![image](../images/portal/certificate-ordered.PNG)

- When this is done, the SSL/TLS certificate will be displayed in the certificates list.

![image](../images/portal/certificate-list.PNG)

# Accessing the TLS/SSL Certificate

- To access the certificate, click the **Details** button in the certificates list page.

- You can download the certificate in .PFX, .CER, .CRT or .PEM formats.

![image](../images/portal/certificate-download.PNG)

- You can also download the Certificate files required for installation in specific web servers (Apache, Apache Tomcat, NGINX, etc). The files include :

- Certificate Private Key (.key)
- Primary Certificate (.crt)
- Intermediate Certificate (CA Bundle) (.crt)
- Full Chain Certificate (.crt)

![image](../images/portal/certificate-download-webserver.PNG)

# Certificate Installation

You will need to manually download and install your certificate in your web server. The following links provides instructions on how to install the certificate in a web server

- [Installing SSL/TLS Certificates in Web Servers and Hosting Services](../installations/web-servers)
- [Installing SSL/TLS Certificates in Apache Server](../installations/apache)
- [Installing SSL/TLS Certificates in Apache Tomcat](../installations/apache-tomcat)
- [Installing SSL/TLS Certificates in NGINX](../installations/nginx)
- [Installing SSL/TLS Certificates in IIS](../installations/iis)

# Certificate Renewal

When a certificate is close to expiration, you should delete the certificate and create a new one.

# Rate Limits

**There is a rate limit of 50 SSL/TLS certificates per subscription.**

In addition, Let's Encrypt has instituted rate limits to ensure fair usage by as many people as possible. To find out more about these rate limits please refer to the following link :

- [Let's Encrypt Rate Limits](https://letsencrypt.org/docs/rate-limits/)


