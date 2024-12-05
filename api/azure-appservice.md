---
title: Azure App Service
description: API for creating a certificate for an Azure App Service
parent: API
nav_order: 7
---

# Azure App Service Certificate
**V8.0**

In this section, you will learn how to create and install a [Certificate in Azure App Service](../portal/azure-appservice.md) (including [SAN](../portal/azure-appservice-san.md)) using the [RCL SSL API](./api.md).

## Prerequisites

Before you can use the API, you must first :

- Obtain an [API Key](./authorization.md)
- Create the [CSR Information](../portal/csr-info.md)

## Authorization

Obtain the [API Key](./authorization.md) in the **Subscription > API Key** page in the RCL SSL Portal.

You must include the API Key in the authorization header of a request as a **Bearer Token**.

## API Endpoint

The endpoint for making API requests is :

- https://rclapi.azure-api.net

## Subscription

To make a request to the API, you must use your subscription. You can obtain the subscription value from the **Subscription > Details** page in the RCL SSL Portal.

![image](../images/api_authorization/subscription.png)

## Getting an Azure Access Token

To access resources in your Azure account (eg. Web App, Function App, Subscription, etc) , you must get an Azure Access Token.

Register a [Microsoft Entra ID Application ](../authorization/aad-application.md) and obtain the following credentials from the application :

```bash
- Client ID (Application ID)
- Tenant ID (Directory ID)
- Client Secret
```

Set [Access Control](../authorization/access-control-app.md) for your application to access your Azure Subscription that contains your Azure resources (eg. Web App, Function App, etc)

To obtain an access token, send a **POST** request to the Microsoft endpoint :

```bash
https://login.microsoftonline.com/{your-tenantid}/oauth2/token
```

Include your credentials in the body of your request as x-www-form-urlencoded

```bash
client_id={your-client-id}&resource=https://management.core.windows.net&client_secret={your-client-secret}&grant_type=client_credentials
```

### Example Request

```bash
POST /547599-bc546-6574-hgf5-rtb-57ls8548hr/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=gjj5ng9-64yhd-laogr-yt45-bjfhatrn45&resource=https://management.core.windows.net&client_secret=djfFrD~7tyHFDSmf_jdfvepgn_hhdbrgr3uHSvd&grant_type=client_credentials

```
### Example Response

```json
{
    "token_type": "Bearer",
    "expires_in": "3599",
    "ext_expires_in": "3599",
    "expires_on": "1733332372",
    "not_before": "1733328472",
    "resource": "00000002-0000-0000-c000-000000000000",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Inp4ZWcyV09OcFRrd041R21lWWN1VGR0QzZKMCIsImtpZCI6Inp4ZWcyV09OcFRrd041R21lWWN1VGR0QzZKMCJ9.eyJhdWQiOiIwMDAwMDAwMi0wMDAwLTAwMDAtYzAwMC0wMDAwMDAwMDAwMDAiLCJpc3MiOiJodHRwczo"
}
```

You can now obtain the access token from the 'access_token' property in the response.

## Create a Certificate using the HTTP challenge

Before you use the API, ensure you [Take the necessary Precautions in your App Service](../portal/azure-appservice.md#http-validation-precautions) . In addition, you should can configured your [Custom Domain](../portal/azure-appservice.md#add-a-custom-domain-to-your-app-service) for your App Service.

To create a certificate using RCL SSL API, send a **POST** request to :

```bash
/prod/v3/ssl/certificate/subscription/{your-subscription}/schedule/create
```

Include a [Certificate object](./certificate-object.md) in the body of the request in jSON format. The following example shows the required fields for the object.

```json
{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "http",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Azure App Service",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJK....",
    "azureAppServiceSiteName": "shopeneur"
}

{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "http",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Azure App Service",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJKV1Q...",
    "azureAppServicePlanName" : "standardAppPlan",
    "azureAppServicePlanResourceGroup" : "webRG",
    "azureAppServiceResourceGroup" : "shopeneurRG",
    "azureAppServiceName": "shopeneur",
    "azureAppServiceSlotName" : ""
}
```

For an App Service in a slot , the site name should be set to : sitename/slotname , eg. shopeneur/dev 

### Example Request

```bash

POST /prod/v3/ssl/certificate/subscription/subscr-0000/schedule/create HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json
Authorization: Bearer resdfre-t435-dkjh-5re6
Content-Length: 1920

{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "http",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Azure App Service",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1...",
    "azureAppServicePlanName" : "standardAppPlan",
    "azureAppServicePlanResourceGroup" : "webRG",
    "azureAppServiceResourceGroup" : "shopeneurRG",
    "azureAppServiceName": "shopeneur",
    "azureAppServiceSlotName" : ""
}
```

After you make the post request, a ```200 OK``` response will be returned. 

### Example Response

```bash
200 OK
```

Your certificate will be scheduled for creation at a later time. 

After a few minutes, you can access your new certificate using the [Get Certificate API](get-certificate.md) .
You should check the App Service custom domain section to ensure the certificate was installed in the App Service.

## Create a Certificate using the DNS challenge

When you create a certificate for an App Service using the [DNS challenge](../portal/azure-appservice.md#create-a-ssltls-certificate-using-dns) , you must use your Azure DNS Zone to create the certificate.

You should can configured your [Custom Domain](../portal/azure-appservice.md#add-a-custom-domain-to-your-app-service) for your App Service.

To create a certificate using RCL SSL API, send a **POST** request to :

```bash
/prod/v3/ssl/certificate/subscription/{your-subscription}/schedule/create
```

Include a [Certificate object](./certificate-object.md) in the body of the request in jSON format. The following example shows the required fields for the object.

```json
{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Azure App Service",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJS...",
    "dnsZoneResourceGroup": "shopeneurRG",
    "azureAppServicePlanResourceGroup" : "webRG",
    "azureAppServicePlanName" : "standardAppPlan",
    "azureAppServiceResourceGroup" : "shopeneurRG",
    "azureAppServiceName": "shopeneur",
    "azureAppServiceSlotName" : ""
}
```

For an App Service in a slot , the site name should be set to : sitename/slotname , eg. shopeneur/dev

### Example Request

```bash

POST /prod/v3/ssl/certificate/subscription/subscr-0000/schedule/create HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json
Authorization: Bearer resdfre-t435-dkjh-5re6
Content-Length: 1965

{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Azure App Service",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGci....",
    "dnsZoneResourceGroup": "shopeneurRG",
    "azureAppServicePlanResourceGroup" : "webRG",
    "azureAppServicePlanName" : "standardAppPlan",
    "azureAppServiceResourceGroup" : "shopeneurRG",
    "azureAppServiceName": "shopeneur",
    "azureAppServiceSlotName" : ""
}
```

After you make the post request, a ```200 OK``` response will be returned. 

### Example Response

```bash
200 OK
```
Your certificate will be scheduled for creation at a later time. 

After a few minutes, you can access your new certificate using the [Get Certificate API](get-certificate.md) .
You should check the App Service custom domain section to ensure the certificate was installed in the App Service.

## Update a Certificate about to Expire

To update a certificate about to expire, send a **POST** request to :

```bash
/prod/v3/ssl/certificate/subscription/{your-subscription}/schedule/update
```

Include a [Certificate object](./certificate-object.md) in the body of the request in jSON format. The following example shows the required fields for the object.

```json
{
    "certificateName" : "shopeneur.com",
    "accessToken": "eyJ0eXAiOiJKV1QiLCJhbGciOiJS..."
}
```

### Sample Request

```bash
POST /prod/v3/ssl/certificate/subscription/subscr-0000/schedule/update HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json
Authorization: Bearer resdfre-t435-dkjh-5re6
Content-Length: 1397

{
    "certificateName" : "shopeneur.com",
    "accessToken": "eyJ0eXAiOiJK..."  
}
```

After you make the post request, a ```200 OK``` response will be returned. 

### Example Response

```bash
200 OK
```
Your certificate will be scheduled for update at a later time. 

After a few minutes, you can access your updated certificate using the [Get Certificate API](get-certificate.md) .
You should check the App Service custom domain section to ensure the certificate was installed in the App Service.

## Error Handling

Errors in the API will be returned as plain text in the body of a response, usually with a ```400 Bad Request```

### Example Response

```bash
Certificate name is not defined.
```