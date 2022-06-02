---
title: Certificate Get
description: RCL Core API - Get a SSL/TLS certificate
parent: RCL Core API
nav_order: 7
---

# Certificate Get
**V6.0.10**

The **Certificate Get API** get a SSL/TLS certificate from a [finalized order](./order-finalize.md).

# Authorization

An access token must be acquired to make requests to the API. Please follow the instructions in the link below to acquire the token.

[Access Token](./authorization.md)

# Subscription Id

Each request must include the **Subscription Id** of the user's subscription in the RCL Portal as a parameter in the request url. You can acquire the Subscription Id in the **Subscription Details** section in the RCL Portal.

![image](../images/autorenew_configure/add_subscriptionid.png)

- Scroll down and copy the 'Subscription Id' 

![image](../images/autorenew_configure/add_subscriptionid2.png)

# Base URI

The base URI for the RCL Core API is :
```
https://rclapi.azure-api.net
```

# API Endpoint and Method

The endpoint for the **Certificate Get** API is :

```
/production/ssl/core/v1/certificate/subscription/{subscriptionid}/get
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the user's subscription in the RCL Portal.

A ``GET`` request must be made to the endpoint.

# Request Parameter

The the name of the certificate must be included in a parameter named ``name`` in the request url.

## Example Request

```
GET /production/ssl/core/v1/certificate/subscription/subscr9836/get?name=www.shopeneur.com HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLC..Vrulj8Xabubg
```

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Core API. A [Certificate](./models.md#certificate) entity to represent the certificate is provided in the **body** of the response in JSON format.

## Example Response Body

```
{
    "certificateName": "www.shopeneur.com",
    "issueDate": "2022-06-01T19:34:06.3563456",
    "expiryDate": "2022-08-30T19:34:06.356435",
    "pfxPassword": "pwd1234",
    "pfxString": "MIACAQMwgAYJK...5AH",
    "certificateDownloadUrls": {
        "pemUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da007cf8...%3D",
        "pfxUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da007c...DA%3D",
        "cerUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da007c...oI%3D",
        "crtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da00...%3D",
        "txtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da00...Y%3D",
        "keyUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da00...E%3D",
        "certCrtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da00...U%3D",
        "cabundleCrtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da00...%3D",
        "fullchainCrtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/da00...A%3D"
    }
}
```

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 404 Not Found

The certificate was not found.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.