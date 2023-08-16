---
title: POST Certificate Renew
description: RCL SSL API - POST Certificate Renew
parent: RCL SSL API
nav_order: 6
---

# POST Certificate Renew
**V7.0.0**

The **Certificate Renew API** will schedule a certificate for renewal. The certificate will be renewed within an hour.

# Authorization

Authorization tokens for **Azure Resource Manager** and **Azure Key Vault** must be acquired to make requests to the API. Please follow the instructions in the link below to acquire both these tokens.

[Authorization Tokens](./authorization.md)

# Subscription Id

Each request must include the **Subscription Id** of the user's subscription in the RCL Portal as a parameter in the request url. You can acquire the Subscription Id in the **Subscription Details** section in the RCL Portal.

![install](../images/autorenew_configure/add_subscriptionid.png)

- Scroll down and copy the 'Subscription Id' 

![install](../images/autorenew_configure/add_subscriptionid2.png)

# Base URI

The base URI for the RCL Public API is :
```
https://rclapi.azure-api.net
```

# API Endpoint

The endpoint for the **POST Certificate Renew** API is :

```
/public/v1/subscription/{subscriptionid}/public/certificate/renew
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the subscription in the RCL SSL Portal.

# Request Body

The request body should include a JSON of the [CertificateRequest](./models.md#certificaterequest) class.

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Public API and scheduling the certificate for renewal. 

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.

# Example Request

```
POST /public/v1/subscription/849/public/certificate/renew HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json

{
    "accessToken" : "eyJ0eXAiOiJk....ww",
    "accessTokenKeyVault" : "eyJ0eXAiOZ....DQ",
    "certificate" : {
        "certificateName": "shopeneur.com"
    }
}
```