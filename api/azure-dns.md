---
title: Azure DNS
description: API for creating a certificate using and Azure DNS Zone
parent: API
nav_order: 5
---

# Azure DNS Certificate
**V8.0**

In this section, you will learn how to create a [Certificate using an Azure DNS Zone](../portal/azure-dns.md) (including [SAN](../portal/azure-dns-san.md)) with the [RCL SSL API](./api.md).

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

To access resources in your Azure account (eg. DNS Zone, Subscription, etc) , you must get an Azure Access Token.

Register a [Microsoft Entra ID Application ](../authorization/aad-application.md) and obtain the following credentials from the application :

```bash
- Client ID (Application ID)
- Tenant ID (Directory ID)
- Client Secret
```

Set [Access Control](../authorization/access-control-app.md) for your application to access your Azure Subscription that contains
your Azure resources (eg. DNS Zone, etc)

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

## Create a Certificate

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
    "target": "Azure DNS",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJKV1QiLCJhb...",
    "dnsZoneResourceGroup": "shopeneurRG"
}
```
### Example Request

```bash
POST /prod/v3/ssl/certificate/subscription/subscr-0000/schedule/create HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json
Authorization: Bearer resdfre-t435-dkjh-5re6
Content-Length: 1689

{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Azure DNS",
    "isSAN": false,
    "azureSubscriptionId": "650085hg4-y6u4-875yh-63hs-hfhg73djgrnd",
    "accessToken": "eyJ0eXAiOiJKV1QiLCJ....",
    "dnsZoneResourceGroup": "shopeneurRG"
}
```

After you make the post request, a ```200 OK``` response will be returned. 

### Example Response

```bash
200 OK
```

Your certificate will then be scheduled for creation at a later time. 

After a few minutes, you can access your new certificate using the [Get Certificate API](get-certificate.md)