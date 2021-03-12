---
title: Automation Systems
parent: API
nav_order: 7
---

# Recommendations for Automation System Design

A developer can use the [RCL API](../api/api) or [RCL SDK](../sdk/sdk) to design an automation system to download and install TLS/SSL certificates in web servers and renew the certificates before they expire. In this section, we will provide recommendation on building such an automation system.

## Primary Usage

The APIs/SDK can be used to build an application to save a certificate in a Widows or Linux Server in a Virtual Machine or Container. The certificate will be used by a web server such as Apache, Apache Tomcat, NGINX or IIS. The application will also automate the renewal of the certificate before it expires.

## Conceptual Design for an Automation System

### Recommendation 1 - Renew Certificates

You can send a POST request to the [CertificateRenewal API](./post-certificate-renewal) to renew certificates. The system can periodically make the request once or twice a week to look for certificate about to expire and renew them.

### Recommendation 2 - Identify Certificates that were Renewed and not Saved in the Server

Wait for about 10 minutes for the certificates to actually renew after making the POST request to the [CertificateRenewal API](./post-certificate-renewal). 

Determine the certificates that were renewed and not saved on the server by making a GET request to the [Certificate List API](./get-certificate-list). These certificates that were not saved on the server will have a **null** value in the ``remoteCreateDate`` property.

### Recommendation 3 - Save Renewed Certificates in the Server

For each of the renewed certificates that were identified in 'Recommendation 2', save the relevant certificate files in a folder on the server for use by the web server (Apache, Apache Tomcat, NGINX, IIS) in a suitable folder in the server (windows or Linux). 

The folder must have the appropriate read/write permissions for the system to write to it and for web server to read from it.

### Recommendation 4 - Update (Flag) the Certificate to Indicate that it was Saved in the Server

For each certificate that was saved in the Server, send a POST request to the [Certificate API](./post-certificate) including a [CertificateResponse](./get-certificate#certificateresponse-object) object in the body with the ``remoteCreateDate`` property set to the date that the certificate was saved. In this way, you can 'flag' certificates that were saved in the server. 

## Algorithm

The following algorithm illustrates a possible automation system design :

```
// Recommendation 1 : Renew certificates

POST CertificateRenewal

// Recommendation 2 : Identify Certificates that were actually renewed and not saved in the server

Wait 10 mins

ListOfCertificateResponse = GET CertificateList

foreach CertificateResponse in ListOfCertificateResponse

    if CertificateResponse.remoteCreateDate == null

        // Recommendation 3 : Save certificate in sever 
        
        SaveCertificateFilesToDirectory

        // Recommendation 4 : Flag a certificate saved in the server

        POST Certificate
            Certificate.remoteCreateDate = "12/10/21T02:20:10"


```

The automation system based on this algorithm can be run once or twice each week.

## Related Articles

- [Introduction to RCL API](./introduction)
- [Authorization: Obtaining an Access Token](./authorization)
- [GET Certificate](./get-certificate)
- [GET CertificateList](./get-certificate-list)
- [POST CertificateRenewal](./post-certificate-renewal)
- [POST Certificate](./post-certificate)