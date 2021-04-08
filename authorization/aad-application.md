---
title: AAD Application
description: Learn how to create an Azure Active Directory Application for use in RCL applications
parent: Authorization
nav_order: 4
---

## Register an AAD Application

**Authorization** is required for the following operations :

- to install SSL/TLS certificates in an App Services , Key Vault and DNS Zone
- to make authorized requests to the [RCL API](../api/api)
- to use the [RCL SDK](../sdk/sdk)
- to use the [RCL AutoRenew](../autorenew/autorenew) Function app
- to use the [RCL CertificateBot](../certbot/certbot)

 This authorization will be granted through an **AAD Application**.

- In the **Azure Active Directory (AAD)**, add a new 'App registration'

![install](../images/authorization_aad_app/create.PNG)

- Add a name for the  new App registration. The app should access accounts in the user's organizational directory only (Single tenant)

![install](../images/authorization_aad_app/create2.PNG)

- Click the 'Register' button 

## Get the AAD Application Credentials

- In the Active Directory, open the application that was registered

- Copy the **Application (client) ID** [Auth:client_id] and **Directory (tenant) ID** [Auth:tenantId] for configuration purposes

![install](../images/authorization_aad_app/aad_app.PNG)

- In the 'Certificates & secrets', create a new client secret

![install](../images/authorization_aad_app/aad_app2.PNG)

![install](../images/authorization_aad_app/aad_app3.PNG)

- Copy the Client Secret **Value** for configuration purposes [Auth:client_secret] 

![install](../images/authorization_aad_app/aad_app4.PNG)

## Next Step

- [Set Access Control for the AAD application](./access-control-app)