---
title: POST Certificate Test
description: RCL API - POST Certificate Test
parent: API
nav_order: 4
---

# POST Certificate Test
**V6.0.10**

The **Certificate Test API** will test the authorized connectivity to the RCL Public API.

# Authorization

Authorization tokens for **Azure Resource Manager** and **Azure Key Vault** must be acquired to make requests to the API. Please follow the instructions in the link below to acquire both these tokens.

[Authorization Tokens](./authorization.md)

# Subscription Id

Each request must include the **Subscription Id** of the user's subscription in the RCL Portal as a parameter in the request url. You can acquire the Subscription Id in the **Subscription Details** section in the RCL Portal.

![install](../images/autorenew_configure/add_subscriptionid2.png)

# Base URI

The base URI for the RCL Public API is :
```
https://rclapi.azure-api.net/public
```

# API Endpoint

The endpoint for the **POST Certificate Test** API is :

```
/v1/subscription/{subscriptionid}/public/certificate/test
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the subscription in the RCL Portal.

# Request Body

The request body should include a JSON of the [ResourceRequest](./models.md#resourcerequest) class.

# Response

## 200 Ok

This represents success in making an authorized connection to the RCL Public API.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.

# Example Request

```
POST /public/v1/subscription/subscr-34001/public/certificate/test HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json

{
    "accessToken" : "eyJ0eXAiOiJk..ww",
    "accessTokenKeyVault" : "eyJ0eXAiOZ..DQ"
}
```



