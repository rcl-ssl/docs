---
title: AAD Application
description: Learn how to create an Azure Active Directory Application for use in RCL applications
parent: Authorization
nav_order: 4
---

## Register a Microsoft Entra (formerly AAD) Application
**V8.0**

**Azure Authorization** is required for the following operations :

- to access Azure resources such as Key Vault, DNS Zone and App Service in a user's Azure Subscription
- to use the [RCL SSL AutoRenew](../autorenew/autorenew) Function app
- to use the [RCL SSL API](../api/api.md) app
- to use the [RCL SSL SDK](../sdk/sdk.md) app


 This authorization will be granted through an **Application**.

- In your **Microsoft Entra ID** tenant in Azure, add a new 'App registration'

![install](../images/authorization_aad_app/create.PNG)

- Add a name for the  new App registration. The app should access accounts in the user's organizational directory only (Single tenant)

![install](../images/authorization_aad_app/create2.PNG)

- Click the 'Register' button 

## Get the Application Credentials

In this section, the following credentials will be obtained from the application :

    - Client ID (Application ID)
    - Tenant ID (Directory ID)
    - Client Secret
    

- In Microsoft Entra ID, open the application that was registered

- Copy the **Application (client) ID** and **Directory (tenant) ID** for configuration purposes

![install](../images/authorization_aad_app/aad_app.PNG)

- In the 'Certificates & secrets', create a new client secret. You must remember to change the client secret when it expires. It is recommended that you use the maximum expiry period (24 months) for the secret.

![install](../images/authorization_aad_app/aad_app2.PNG)

![install](../images/authorization_aad_app/aad_app3.PNG)

- Copy the Client Secret **Value** for configuration purposes  

![install](../images/authorization_aad_app/aad_app4.PNG)
