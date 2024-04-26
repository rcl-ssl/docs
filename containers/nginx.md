---
title: NGINX with SSL/TLS
description: RCL SSL DNS AutoRenew for Docker and NGINX 
parent: Containers
nav_order: 2
---

# RCL SSL DNS AutoRenew for Docker and NGINX

NGINX can use SSL/TLS certificates saved to a volume by RCL SSL DNS AutoRenew for Docker. In this way, you can enable SSL/TLS for a web application hosted with docker.

{: .information }
Before you can use [RCL SSL DNS AutoRenew for Docker](./docker.md), you must have already created your certificate(s) in the RCL SSL Portal using the [Azure DNS](../portal/azure-dns.md) or [Azure DNS SAN](../portal/azure-dns-san.md) option. The certificate(s) that you would like to install must be specified in your [configuration](./docker.md#notes) of RCL DNS AutoRenew for Docker.

# Prerequisites

Follow the link in the instruction below to Configure, Install and Test RCL SSL DNS AutoRenew for Docker.

- [RCL SSL DNS AutoRenew for Docker](./docker.md)

# Configure NGINX to use SSL/TLS

{: .information }
You can download the files used in this sample from GitHub:
[NGINX with SSL/TLS Docker](https://github.com/rcl-ssl/nginx-with-ssl-docker)

Firstly, we will create a configuration file for NGINX to accept SSL/TLS connection on port 443.

- Create a folder named ``nginx``

- In the ``nginx`` folder, create a configuration file named ``nginx.conf``

- In the ``nginx.conf`` file add the following configuration

```bash
server {
  listen 80;
  server_name example.com;
}

server {
    listen              443 ssl;
    server_name         example.com;
    ssl_certificate     /etc/ssl/rcl/example-com/fullChainCertificate.crt;
    ssl_certificate_key /etc/ssl/rcl/example-com/privateKey.key;
}
```

- This is a minimalist configuration file, you can amend it with additional configuration to meet your requirements

- Replace ``example.com`` with your domain name

- RCL SSL DNS AutoRenew will auto generate folder names to store certificate files. In this case, for the domain ``example.com``, the full chain certificate and private key files are stored in a folder named ``example-com`` following a folder naming convention. For your domain, follow the [Folder Naming Convention](./docker.md#certificate-files) described in this link

## Create a Docker Compose file

- Create a file named ``compose.yaml``

- Add the following code to the file

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
      - CertificateBot__IncludeCertificatesArray=example.com
    volumes:
      - rclssl-certs:/etc/ssl/rcl
  nginx:
    image: nginx:latest
    ports:
      - 80:80
      - 443:443
    restart: always
    volumes: 
      - ./nginx/nginx.conf:/etc/nginx/conf.d/default.conf
      - rclssl-certs:/etc/ssl/rcl
    depends_on:
      - rclssldnsautorenew
volumes:
  rclssl-certs:
    driver: local
```

- Firstly, the RCL SSL DNS AutoRenew service is deployed. It will save TLS/SSL certificates from the RCL SSL Portal to a docker volume shared with NGINX

-  Then, the NGINX service is deployed, it uses the ``nginx.conf`` file we created to accept SSL/TLS connections

- NGINX uses the SSL/TLS certificate files stored on the docker volume that were saved by RCL SSL DNS AutoRenew

- You should add you own [Configuration Values](./docker.md#configuration-prerequisite) eg, client-id, etc. for RCL SSL DNS AutoRenew service

- Replace ``example.com`` with you own domain name

# Deploy the Container

- Open a terminal window in your folder

- Run the following command to deploy the container

```bash
docker compose -f compose.yaml -d
```

- View the [Log Files](./docker.md#view-the-logs) to see it there are any errors in the RCL SSL DNS AutoRenew service

- Ensure the SSL/TLS is successfully installed in NGINX by viewing your website in a browser and checking the SSL/TLS certificate

![image](../images//container//browser-ssl.png)