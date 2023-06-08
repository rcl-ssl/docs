﻿---
title: AAD Application
description: Learn how to create an Azure Active Directory Application for use in RCL applications
parent: Authorization
nav_order: 4
---

## Register an AAD Application
**V7.0.0**

**Authorization** is required for the following operations :

- to access Azure Key Vault, DNS Zone and App Service in a user's Azure account
- to use the [RCL SSL AutoRenew](../autorenew/autorenew) Function app
- to make authorized requests to the [RCL SSL API](../api/api.md)
- to use the [RCL SSL SDK](../sdk/sdk.md)
- to use the [RCL SSL CertificateBot](../certbot/certbot.md)

 This authorization will be granted through an **AAD Application**.

- In your **Azure Active Directory (AAD)** tenant, add a new 'App registration'

![install](../images/authorization_aad_app/create.PNG)

- Add a name for the  new App registration. The app should access accounts in the user's organizational directory only (Single tenant)

![install](../images/authorization_aad_app/create2.PNG)

- Click the 'Register' button 

## Get the AAD Application Credentials

In this section, the following credentials will be obtained from the AAD application :

    - Client ID (Application ID)
    - Tenant ID (Directory ID)
    - Client Secret
    

- In the Active Directory, open the application that was registered

- Copy the **Application (client) ID** [Auth:client_id] and **Directory (tenant) ID** [Auth:tenantId] for configuration purposes

![install](../images/authorization_aad_app/aad_app.PNG)

- In the 'Certificates & secrets', create a new client secret. You must remember to change the client secret when it expires. It is recommended that you use the maximum expiry period (24 months) for the secret.

![install](../images/authorization_aad_app/aad_app2.PNG)

![install](../images/authorization_aad_app/aad_app3.PNG)

- Copy the Client Secret **Value** [Auth:client_secret] for configuration purposes  

![install](../images/authorization_aad_app/aad_app4.PNG)


## Related Articles
- [Set Access Control for the AAD application](./access-control-app)
- [RCL SSL AutoRenew Function](../autorenew/autorenew.md)
- [RCL SSL CertificateBot](../certbot/certbot.md)
- [RCL SSL API](../api/api.md)
- [RCL SSL SDK](../sdk/sdk.md)