---
title: Linux Daemon
description: RCL SSL CertificateBot Linux Daemon for automatic SSL/TLS certificate installation and renewal in a Linux server 
parent: RCL SSL CertificateBot
nav_order: 2
---

# RCL SSL CertificateBot for Linux
**V7.0.0**

RCL SSL CertificateBot runs as a **Daemon** in a Linux hosting machine. The daemon will run every seven (7) days to automatically renew and save SSL/TLS certificates from a user's subscription in the **RCL SSL Portal** to the Linux hosting machine.

## Automatically Renew SSL/TLS Certificates

You can use RCL SSL CertificateBot to automatically renew SSL/TLS certificates created in the **RCL SSL Portal** using the the following creation options :

- [Azure DNS](../portal//azure-dns.md) (including [SAN](../portal/azure-dns-san.md)) 

**'Stand Alone' certificates are not supported by RCL SSL CertificateBot.**

# Installing RCL SSL CertificateBot

## Download and Extract the Daemon Files to the Linux Server

In this section, you will download the files from the RCL SSL CertificateBot [GitHub Project Page](https://github.com/rcl-ssl/RCL.CertificateBot) in the [Releases](https://github.com/rcl-ssl/RCL.CertificateBot/releases) section; and extract it to your Linux Server in the ``/usr/sbin`` folder:

- In your Linux server, navigate to the ``/usr/sbin`` folder

```bash
cd /usr/sbin
```

- Run the command in the folder to download and extract the ``linux-x64`` files:

```bash
wget -c https://github.com/rcl-ssl/RCL.CertificateBot/releases/download/V6.0.10/certificatebot-linux-x64.tar.gz -O - | sudo tar -xz
```

or ``linux-arm`` files :

```bash
wget -c https://github.com/rcl-ssl/RCL.CertificateBot/releases/download/V2.1/certificatebot-linux-arm.tar.gz -O - | sudo tar -xz
```

## Configure the Daemon

### Register an AAD Application

An Azure Active Directory (AAD) application must be registered to obtain permission to access a user's Azure resources (**DNS Zone**). 

Please refer to the following link to register an AAD application:

- [Registering an AAD Application](../authorization/aad-application)

### Set Access Control for the AAD Application

Access control must be set for the AAD application to access resources (**DNS Zone**) in a user's Azure subscription. Please refer to the following link to set access control :

- [Setting Access Control for the AAD Application](../authorization/access-control-app)

### Get the AAD Application Credentials 

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


## Add the Configuration variables

- Navigate to the folder you downloaded and extracted the daemon files :

```bash
cd /usr/sbin/certificatebot-linux-x64
```

or for ``arm``

```bash
cd /usr/sbin/certificatebot-linux-arm
```

- Use nano (or other text editor) to edit the **appsettings.json** file in the folder

```bash
sudo nano appsettings.json
```

- Add the credentials for the AAD Application and SubscriptionId in the **RCLSDK** section :
  - ClientId
  - ClientSecret
  - TenantId
  - SubscriptionId

- In the **CertificateBot** section, set a folder path to save the SSL/TLS certificates. Recommended path : /etc/ssl/certificatebot

  - saveCertificatePath

- The ``includeCertificates`` settings will allow for including specific certificates by its name 
(eg:  "contoso.com"  or "contoso.com, *.contoso.com" - for SAN) for the certificate(s) you want to save on the server. 

Example
```json
  "CertificateBot": {
    "saveCertificatePath": "/etc/ssl/certificatebot",
     "includeCertificates": [
       "contoso.com",
       "fabricam.com",
       "acme.com,*.acme.com",
       "adworks.com, www.adworks.com"
       ]
  },
```

## Example of a configured **appsettings.json** file

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "RCLSDK": {
    "ApiBaseUrl": "https://rclapi.azure-api.net/public",
    "SourceApplication": "RCL SSL CertificateBot Linux",
    "ClientId": "35ca82aa-9ff3-5a67-bb7f-c3c71027eecf",
    "ClientSecret": "hdytev539dgw~_8-g4lNI84V01.yIDUMHh",
    "TenantId": "22cd4a8c-bc2c-3618-b1c3-4610c1b9b3e8",
    "SubscriptionId": "879"
  },
  "CertificateBot": {
    "SaveCertificatePath": "/etc/ssl/certificatebot",
    "IncludeCertificates": [
      "shopeneur.com,*.shopeneur.com"
    ],
    "IISBindings": []
  }
}
```
- Save the updated **appsettings.json** file when you are done

- Create the folder in the server and ensure it has read/write permissions so that the certificates can be saved to it. 

```bash
sudo mkdir -m 777 /etc/ssl/certificatebot
```

# Add the Linux Daemon

## Create the Daemon

- Navigate to the **/etc/systemd/system** folder

```bash
cd /etc/systemd/system
```

- Create the daemon file

```bash
sudo touch certificatebot.service
```

- Use nano (or other text editor) to edit the service file 

```bash
sudo nano certificatebot.service
```

- Add the following code to the file

```bash
[Unit]
Description=RCL CertificateBot

[Service]
Type=notify
WorkingDirectory=/usr/sbin/certificatebot-linux-x64
ExecStart=/usr/sbin/certificatebot-linux-x64/RCL.SSL.CertificateBot.Linux

[Install]
WantedBy=multi-user.target

```

If you installed the ``arm`` version, change the directory to the arm path ``/usr/sbin/certificatebot-linux-arm`` instead of ``/usr/sbin/certificatebot-linux-x64`` in the 'WorkingDirectory' and 'ExecStart' settings

- Save the file when you are done

## Reload the Daemon

- Reload the daemon anytime you make changes to the service file

```bash
sudo systemctl daemon-reload
```

## Start the Daemon

- Run the code to start the daemon

```bash
sudo systemctl start certificatebot
```

## View the Status of the Daemon

- Run the code to view the status of the daemon

```bash
sudo systemctl status certificatebot
```

- You will see the status of the daemon. The most recent logs will also be displayed. 

- Ensure that there are no errors in the logs. If there are errors, the daemon is misconfigured and will not function

## View the Detailed Logs

- Run the command to view the daemon's detailed logs

```bash
sudo journalctl -u certificatebot --no-pager
```

- If the application is working correctly you should see messages similar to the one below :

```bash
RCL.SSL.CertificateBot.Linux.Worker[0] Found 1 certificate(s) to save locally.  Successfully saved : shopeneur.com,*.shopeneur.com.  Did not find any certificates to renew.
```

## If you need to Stop the Daemon

- Run the code if you need to stop the daemon (in case you need to update settings or fix errors). 

When the daemon is stopped, CertificateBot will discontinue certificate renewals and installation in the server.

**Note: You need to keep the daemon running to automatically renew certificates.**

```bash
sudo systemctl stop certificatebot
```

# Fixing Errors

If you encounter errors in the logs for the daemon, please stop the daemon. Ensure the 'appsettings' configuration is correct for the AAD Application credentials and the certificate save path settings. 

The folder to save the certificate must have read/write access. 

Reload and restart the daemon after you make changes and check if the errors were resolved.

# Installing Certificates in Web Servers

RCL SSL CertificateBot will automatically save renewed SSL/TLS certificate files to a folder in the server. You should then configure the web server to use these files to implement SSL/TLS in your website.

## Certificate Files

The SSL/TLS certificate files will be stored at the path you specified in the ``appsettings.json`` configuration file. In this example, we used the path ``/etc/ssl/certificatebot`` to store the certificate files.

To view the files

```bash
cd /etc/ssl/certificatebot
```

When configuring the web servers, you will reference the specific certificate files stored at that path in a folder generated by CertificateBot for a specified domain.

The following files are downloaded and saved on the server :

  - ``certificate.pfx`` - The PFX certificate file
  - ``primaryCertificate.crt`` The primary certificate file
  - ``fullChainCertificate.crt`` - The full chain certificate file
  - ``caBundle.crt`` - The intermediate certificate file
  - ``privateKey.key`` - The certificate's private key file

## Configuring the Web Servers

Please follow the links below to configure your web server:

- [Installing SSL/TLS Certificates in Apache Server](../installations/apache)
- [Installing SSL/TLS Certificates in Apache Tomcat](../installations/apache-tomcat)
- [Installing SSL/TLS Certificates in NGINX](../installations/nginx)
- [Installing SSL/TLS Certificates in Web Servers and Hosting Services](../installations/web-servers)


