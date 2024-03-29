---
title: IIS
description: RCL SSL HTTP AutoRenew Windows Service for automatic SSL/TLS certificate installation and renewal in IIS
parent: HTTP AutoRenew
nav_order: 4
---

# RCL SSL HTTP AutoRenew for IIS
**V7.1.0**

RCL SSL HTTP AutoRenew for IIS runs as a **Windows Service** in a Windows hosting machine. The Windows Service will run every seven (7) days to automatically renew and save SSL/TLS certificates from a user's subscription in the **RCL SSL Portal** to the Windows hosting machine.

Certificates will be automatically saved to the ``Local Machine`` certificate store in the  ``Personal`` folder. Certificates will also be automatically bound to the **IIS Web Server** on the hosting machine.

## Automatically Renew SSL/TLS Certificates

You can use the service for IIS to automatically renew SSL/TLS certificates created in the **RCL SSL Portal** using the the following creation options :

- [Stand Alone](../portal/stand-alone.md) (including [SAN](../portal/stand-alone-san.md)) using the [HTTP Challenge](../portal/stand-alone.md#completing-the-http-challenge) type.

# Installation

If you have an older version of the service installed on your hosting machine, you should delete it and install the new service.

## Download the Files

- The Windows Service files (``http-autorenew-iis-xxx``) are available in the [GitHub Project](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal) page in the [Releases](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal/releases/tag/V7.1.0) section:

- Download the zip file with bitness :

  - [win-x64](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal/releases/download/V7.1.0/http-autorenew-iis-x64.zip) 
  - [win-x86](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal/releases/download/V7.1.0/http-autorenew-iis-x86.zip)
  - [win-arm](https://github.com/rcl-ssl/rcl-ssl-automatic-renewal/releases/download/V7.1.0/http-autorenew-iis-arm.zip)
  
  to match your Windows bitness

- Extract the zip file to a folder on your Windows hosting machine after it is downloaded

## Configure the Service

### Create an API Key

The service uses the RCL SSL Core API to renew certificates. You must create an Api Key to make authorized requests to the API. Follow the instructions in the following link to create an Api Key in the RCL SSL Portal.

[Create an Api Key](../apicore/authorization.md)

### Get the SubscriptionId

Get the **Subscription Id** in the RCL SSL Portal.

![install](../images/autorenew_configure/add_subscriptionid.png)

- Scroll down and copy the 'Subscription Id' 

![install](../images/autorenew_configure/add_subscriptionid2.png)


### Add the Configuration variables

- In the folder containing the files for the Windows Service that you extracted, find and open the **appsettings.json** file

- Add the credentials for the Api Key and SubscriptionId in the **RCLSDK** section :

  - Api Key
  - SubscriptionId

Example
```json
"RCLSDK": {
    "ApiBaseUrl": "https://rclapi.azure-api.net/v2",
    "SourceApplication": "RCL HTTP AutoRenew IIS",
    "ApiKey": "xxx",
    "SubscriptionId": "xxx"
  }
```

- In the **CertificateBot** section, set a folder path to save the SSL/TLS certificates. 

  - saveCertificatePath

Example
```json
    "CertificateBot" : {
        "IncludeCertificates":[],
        "SaveCertificatePath": "C:/ssl",
        
    }
  ```

- **Note : when setting any folder path , use forward slashes(``/``) in the path name, eg. ``C:/ssl``. Failure to do this will result in inability to run the windows service.**

- Create the folder on your hosting machine at the path you specified to save the certificates.

- Ensure the folder has read/write permissions so that the certificates can be saved to it. 

- Configure the site bindings for each website that you want to bind a SSL/TLS certificate. You can have a single or multiple bindings.

- Example of multiple bindings (using a [SAN](../portal/stand-alone-san.md) certificate):


- Example of a single binding :

Example
```json
"IISBindings": [
  {
    "siteName":"AdventureWorks",
    "ip":"*",
    "port":"443",
    "host":"adventureworks.com",
    "certificateName":"adventureworks.com",
    "validationPath": "C:/inetpub/adventureworks/wwwroot"
  }
]
```

- Example of multiple bindings :

```json
"IISBindings": [
  {
    "siteName":"Contoso",
    "ip":"*",
    "port":"443",
    "host":"contoso.com",
    "certificateName":"contoso.com,www.contoso.com",
    "validationPath": "C:/inetpub/contoso/wwwroot"
  },
  {
    "siteName":"Contoso",
    "ip":"*",
    "port":"443",
    "host":"www.contoso.com",
    "certificateName":"contoso.com,www.contoso.com",
    "validationPath": "C:/inetpub/contoso/wwwroot"
  },
  {
    "siteName":"Fabricam",
    "ip":"*",
    "port":"443",
    "host":"fabricam.com",
    "certificateName":"fabricam.com",
    "validationPath": "C:/inetpub/fabricam/wwwroot"
  }
]
```


- siteName - this is the **Site** name of the IIS website
- ip - this is the **IP Address** of the IIS website (you can use any (``*``))
- port - the is the **Port** number of the IIS website (you can use ``443``)
- host - the the **Host (Domain) Name** assigned to the IIS website
- certificateName - this is the name of the certificate in the RCL SSL Portal to be installed in the IIS website
- validationPath - the root path to the folder where your website is hosted. This is where the validation tokens will be saved for the HTTP challenge

> The website must be actively served by the web server from the ``validationPath`` and the site must be publicly accessible on the web in a web browser. If these conditions are not met, the SSL/TLS certificate update will fail for the HTTP challenge.

![install](../images/certbot/iis.PNG)

The image above illustrates a site hosted in IIS named 'Home' with multiple bindings. The site is bound to a naked apex domain, 'shopeneur.com', and a sub-domain 'www.shopeneur.com'. The website can be accessed publicly on the web with either of these domains. The site uses the same multi-domain [SAN](../portal/azure-dns-san.md) certificate named : 'shopeneur.com,www.shopeneur.com' to provide SSL/TLS for both the domains.

## Example of a configured **appsettings.json** file

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    },
    "EventLog": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    }
  },
  "RCLSDK": {
    "ApiBaseUrl": "https://rclapi.azure-api.net/v2",
    "SourceApplication": "RCL SSL HTTP AutoRenew IIS",
    "ApiKey": "abc123",
    "SubscriptionId": "ergt546"
  },
  "CertificateBot": {
    "IncludeCertificates":[],
    "SaveCertificatePath": "C:/ssl",
    "IISBindings": [
      {
        "siteName":"Home",
        "ip":"*",
        "port":"443",
        "host":"shopneur.com",
        "certificateName":"shopeneur.com,www.shopeneur.com",
        "validationPath": "C:/inetpub/wwwroot"
      },
      {
        "siteName":"Home",
        "ip":"*",
        "port":"443",
        "host":"www.shopneur.com",
        "certificateName":"shopeneur.com,www.shopeneur.com",
        "validationPath": "C:/inetpub/wwwroot"
      }
    ]
  }
}
```
- Save the **appsettings.json** file when you are done.

# Create the Windows Service

- Open a **Command Prompt** in the Windows hosting machine as an **Administrator**

- Run the following command to install the Windows Service. Replace the < file-path > placeholder with the actual path where your windows service zip files were extracted

```
sc.exe create HttpAutoRenewIIS binpath= <file-path>\RCL.SSL.HTTP.AutoRenew.IIS.exe
```

- After the service in installed, open **Services** in Windows, look for the ``HttpAutoRenewIIS`` service and **Start** the service

![image](../images/http_autorenew/winservice-iis-start.png)

- Set the **Properties** of the service to start automatically when the hosting machine starts

![image](../images/http_autorenew/winservice-iis-automatic.png)

# View the Event Logs

- Open **Event Viewer**, under 'Windows Logs > Application', look for the ``RCL.SSL.HTTP.AutoRenew.IIS`` events

![image](../images/http_autorenew/winservice-iis-event.png)

- Ensure that there are no error events for the service. If there are error events, the service is misconfigured and will not function

- Each time a certificate is renewed, a log will be written

- The service will run every seven (7) days to automatically renew certificates in the IIS web server

# Fixing Errors

If you encounter error events for the service in the Event Viewer, please stop the service and delete it completely. 

Ensure the ``appsettings`` configuration is correct for the ``Api Key`` and the certificate ``Save Path`` settings point to a folder that exists. 

Fix any other errors that are reported. Then, re-install and restart the service.

# Testing Certificate Renewal

## Force Certificate Expiration

In order to test certificate renewal, you must first force certificate expiration in the RCL SSL Portal.

- In the RCL SSL Portal, click on the **SSL/TLS Certificate > Certificates List** link in the side menu

- In the certificates list, click the **Manage > Force Expiry** link

- In the ``Force Expiry`` page, click the **Force Expiry** button

- The certificate will be forced to expire in the next 14 days

![Force Expiry](../images/http_autorenew/force-expiry.png)

## Testing Renewal

- Re-start the service to trigger the certificate renewal

- Open **Event Viewer**, under 'Windows Logs > Application', look for the ``RCL.SSL.HTTP.AutoRenew.IIS`` events

- Ensure that there are no error events for the service

- If there are errors: fix the errors , restart the service to run the test again

- Check that the certificate(s) are bound to the IIS website(s)

- Once this test passes, the service will run every seven days to automatically renew certificates and bind them to the IIS websites

# Deleting the Windows Service

If you need to remove the Windows Service for any reason, first stop the service, then run the command to delete the service

```
sc.exe delete HttpAutoRenewIIS
```

# Updating the Service

If you need to update the service to include other IIS bindings and certificates, follow these steps:

- Stop the service and delete it
- Change the ``appsettings.json`` file to include updated IIS bindings and certificates
- Re-create the service and start it

# Reset the Service

If you need to reset the service because of a error or corrupted certificate renewal, follow these steps :

- Stop the service and delete it
- Delete all certificates and their folders in the directory in which certificates are saved
- Re-create the service and start it


