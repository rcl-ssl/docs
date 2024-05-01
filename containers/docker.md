---
title: Docker
description: RCL SSL DNS AutoRenew for Docker for automatic SSL/TLS certificate installation and renewal 
parent: Containers
nav_order: 1
---

# RCL SSL DNS AutoRenew for Docker
**V7.1.0**

In this section, we will learn how to use the RCL SSL DNS AutoRenew docker image to install and renew SSL/TLS certificates created in the [RCL SSL Portal](../portal//portal.md) in a docker host.

{: .information }
Before you can use RCL SSL DNS AutoRenew for Docker, you must have already created your certificate(s) in the RCL SSL Portal using the [Azure DNS](../portal/azure-dns.md) or [Azure DNS SAN](../portal/azure-dns-san.md) option. The certificate(s) that you would like to install must be specified in your [configuration](#notes) of RCL SSL DNS AutoRenew for Docker.

# Automatically Install and Renew SSL/TLS Certificates

You can use RCL SSL DNS AutoRenew for Docker to automatically install and renew SSL/TLS certificates in a docker host created in the **RCL SSL Portal** using the the following creation options:

- [Azure DNS](../portal//azure-dns.md) (including [SAN](../portal/azure-dns-san.md))

Certificates will be save to a volume on the host machine for an ingress controller to use.

# Configuration Prerequisite

## AAD Application

An Azure Active Directory (AAD) application must be registered to obtain permission to access a user's Azure resources (**DNS Zone**). 

Please refer to the following link to register an AAD application:

- [Registering an AAD Application](../authorization/aad-application)

## Set Access Control for the AAD Application

Access control must be set for the AAD application to access resources (**DNS Zone**) in a user's Azure subscription. Please refer to the following link to set access control :

- [Setting Access Control for the AAD Application](../authorization/access-control-app)

## Get the AAD Application Credentials 

To obtain the following credentials from the AAD application:

- ClientId
- ClientSecret
- TenantId

follow the instructions in this link :

- [Get the AAD Application Credentials](../authorization/aad-application#get-the-aad-application-credentials)

## Get the SubscriptionId

Get the **Subscription Id** in the RCL SSL Portal.

![install](../images/autorenew_configure/add_subscriptionid.png)

- Scroll down and copy the 'Subscription Id' 

![install](../images/autorenew_configure/add_subscriptionid2.png)

## Register the AAD Application's ``Client Id`` in the RCL SSL Portal

The AAD Application must be associated with a user's RCL SSL subscription. This is achieved by registering the AAD Application's ``Client Id`` in the **RCL SSL Portal**.

To add the AAD Application's ``Client Id`` to the portal, please follow the instructions in this link :

- [Add the Client Id in the RCL SSL Portal](../api/authorization#add-the-client-id-in-the-rcl-portal)

# Deploy the Container

## Docker Command

Run the following command to deploy a docker container:

```bash
docker run -d \
--env RCLSDK__ClientId=your-client-id \
--env RCLSDK__ClientSecret=your-client-secret \
--env RCLSDK__TenantId=your-tenant-id \
--env RCLSDK__SubscriptionId=your-subscription-id \
--env CertificateBot__SaveCertificatePath=/etc/ssl/rcl \
--env CertificateBot__IncludeCertificatesArray=shopeneur.com \
--mount source=rclssl-certs,target=/etc/ssl/rcl \
rclssl/dns-autorenew:7.1.0 

```

## Docker Compose

Run the following Docker Compose file to deploy a docker container:

```yaml
version: '3'
services:
  rclssldnsautorenew:
    image: rclssl/dns-autorenew:7.1.0
    environment:
      - RCLSDK__ClientId=your-client-id
      - RCLSDK__ClientSecret=your-client-secret
      - RCLSDK__TenantId=your-tenant-id
      - RCLSDK__SubscriptionId=your-subscription-id
      - CertificateBot__SaveCertificatePath=/etc/ssl/rcl
      - CertificateBot__IncludeCertificatesArray=shopeneur.com
    volumes:
      - rclssl-certs:/etc/ssl/rcl
volumes:
  rclssl-certs:
    driver: local
```

## Notes

- Note the double underscore (__) in the environment variables, eg. ``RCLSDK__ClientId``

- Replace the environment variable values with the ones you obtained in the ``Configuration Prerequisite`` section

- A volume is created to save the certificates files. The volume's target path is set in ``CertificateBot__SaveCertificatePath`` environment variable. The certificates will be available in the volume for a web server or other container(s) to use

- The ``IncludeCertificatesArray`` environment variable will allow for including specific certificates by its name 
(eg:  "contoso.com"  or "contoso.com, * .contoso.com" - for SAN) for the certificate(s) you want to renew and save on the volume. Multiple certificates must be separated by a semi-colon (;), eg. shopeneur.com;acme.com;contoso.com,* .contoso.com

- Run a single container to avoid renewal issues

# View the Logs

- Run the command to view the container's logs

- Specify the id of the container to get the logs

```bash
docker logs containerid
```

- The logs should resemble the sample shown below:

```bash
Message received at : 04/25/2024 20:38:52.  Found 1 certificate(s) to process locally.   Retrieved certificate shopeneur.com.  Saved shopeneur.com locally.  Did not find any certificates to renew.
```

# Fixing Errors

If you encounter errors in the logs for the container, please stop the container. Ensure the environment variables and configuration are correct for the AAD Application credentials and the certificate save path settings. 

Delete and re-create the container after you make changes and check if the errors were resolved.

# Testing Certificate Renewal

## Force Certificate Expiration

In order to test certificate renewal, you must first force certificate expiration in the RCL SSL Portal.

- In the RCL SSL Portal, click on the **SSL/TLS Certificate > Certificates List** link in the side menu

- In the certificates list, click the **Manage > Force Expiry** link

- In the ``Force Expiry`` page, click the **Force Expiry** button

- The certificate will be forced to expire in the next 14 days

![Force Expiry](../images/http_autorenew/force-expiry.png)

## Testing Renewal

- Stop and restart the container to trigger the certificate renewal

- Specify the name of the container 

```bash
docker container stop container-name
docker container start container-name
```

- Run the command to view the container's logs

```bash
docker logs containerid
```

- Check the logs to ensure the certificate is scheduled for renewal. 

- The logs should resemble the sample shown below:

```bash
Message received at : 04/25/2024 21:53:54.  Found 1 certificate(s) to process locally.   Retrieved certificate shopeneur.com.  Saved shopeneur.com locally.  Found certificate : shopeneur.com to renew.   Successfully scheduled certificate shopeneur.com for renewal.
```

- After about 15 mins, stop and re-start the container to save the certificate to the volume

```bash
docker container stop container-name
docker container start container-name
```

- Run the command to view the container's logs

```bash
docker logs containerid
```

- Check the logs to ensure the certificate is scheduled for renewal.

- The logs should resemble the sample shown below:

```bash
Message received at : 04/25/2024 21:57:48.  Found 1 certificate(s) to process locally.   Retrieved certificate shopeneur.com.  Saved shopeneur.com locally.  Did not find any certificates to renew.
```

- Check that the certificate files are stored in the volume that you specified. 

- Specify the volume-name

 ```bash
docker volume inspect vloume-name
 ```

- Once this test passes, the container will run every seven days to automatically renew certificates and save the certificate files to a volume you specify

# Certificate Files

The SSL/TLS certificate files will be stored in the volume you specified.

In the volume, a folder is generated by the container based on the certificate name. All the files for the certificate will be stored in this folder.

For each certificate, the following files are downloaded and saved with the following file names:

  - ``certificate.pfx`` - The PFX certificate file
  - ``primaryCertificate.crt`` - The Primary Certificate file
  - ``fullChainCertificate.crt`` - The full chain certificate file
  - ``caBundle.crt`` - The Intermediate Certificates (CA Bundle) file
  - ``privateKey.key`` - The Certificate Private Key file

   The files are saved in a folder generated by the container based on the certificate name following these conventions :

  |Type               |Example Certificate Name         |Example Folder Name
  |-------------------|---------------------------------|---------------------
  |Apex Domain        |shopeneur.com                    |shopeneur-com
  |Sub-domain         |store.shopeneur.com              |store-shopeneur-com
  |Wildcard domain    |*.shopeneur.com                  |wcard-shopeneur-com
  |SAN HTTP Challenge |shopeneur.com,www.shopeneur.com  |shopeneur-com-san-www
  |SAN DNS Challenge  |shopeneur.com,*.shopeneur.com    |shopeneur-com-san-wcard

# Installing Certificates in Web Servers

Please follow the links below to configure your web server to use the certificates files in the volume generated by the container :

- [RCL SSL AutoRenew for Docker and NGINX](./nginx.md)
