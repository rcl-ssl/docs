---
title: Microsoft IIS
parent: CertificateBot
nav_order: 3
---

# Using RCL CertificateBot with Microsoft IIS

[RCL CertificateBot](./certbot) can be used to automate the installation and renewal of SSL/TLS certificate in Microsoft IIS. This is achieved as follows:

- RCL CertificateBot is configured in the ``appsettings.json`` file to recognize the **bindings** of one or more websites in IIS
- RCL CertificateBot automatically renews certificates and installs the certificates in each binding specified in the configuration

## Installing RCL CertificateBot in Windows

Please follow the instructions in the following link to install RCL CertificateBot in Windows:

- [Installing RCL CertificateBot in Windows](./windows-service)

## Configuring RCL CertificateBot for IIS

The IIS website bindings must be configured in the ``appsettings.json`` file in the ``bindings`` section in ``CertificateBot``. The following is an example shows a single website binding :

```
  "CertificateBot": {
    "saveCertificatePath": "c:/ssl",
    "includeCertificates": [ "all" ],
    "serverIdentifier": "default",
    "bindings": [
      {
        "siteName": "Home",
        "ip": "*",
        "port": "443",
        "host": "shopeneur.com",
        "certificateName": "shopeneur.com"
      }
    ]
  }
```

- siteName - this the the site name of the IIS website
- ip - this is the IP address of the IIS website
- port - the is the port number of the IIS website
- host - the the host name assigned to the IIS website
- certificateName - this is the name of the certificate in the RCL Portal to be installed in the IIS website

You can include more than one bindings in the ``bindings`` array.

The following image illustrates the IIS website and the binding :

![install](../images/certbot/iis.PNG)