---
title: NGINX Server
parent: Certificate Installations
nav_order: 3
---

# Installing TLS/SSL Certificates in NGINX

This article assumes that you have experience with NGINX in Linux or Windows.

## Get the Certificate Files Manually

You can download the files required to install the TLS/SSL certificate in the NGINX web server from the **RCL Portal** on the **Certificate Details** page.

## Get the Certificate Files Automatically

You can also use the [RCL CertificateBot](../certbot/certbot) to automatically renew and download the files required to install the TLS/SSL certificate in the NGINX web server.

## Files Required

The files required are :

- Certificate Private Key (.key)
- Full Chain Certificate (.crt)

## Web Server Configuration

Update your web server configuration (in the : /path-to-nginx/sites-enabled folder) for your site and add these attributes to the sites you want HTTPS on

```
# SSL configuration
listen 443 ssl default_server;
listen [::]:443 ssl default_server;
ssl_certificate  /path/to/fullChainCertificate.crt;
ssl_certificate_key  /path/to/privateKey.key;
```
You can modify the names of the files and paths to match the location and filename that you used to save your certificate files.

Remember to reload the service, or restart if it's a new site.

Linux command
```
sudo systemctl reload nginx
```

Now you can confirm your domain SSL certificate using any of the SSL checker tools available. Or you can just browse the URL.