---
title: Order Get
description: RCL Core API - Get an order for a SSL/TLS certificate
parent: RCL Core API
nav_order: 4
---

# Order Create 
**V6.0.10**

The **Order Get API** will get an order for a SSL/TLS certificate by the Order URI.

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

The endpoint for the **Order Get** API is :

```
production/ssl/core/v1/order/subscription/{subscriptionid}/get
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the user's subscription in the RCL Portal.

A ``POST`` request must be made to the endpoint.

# Request Body

The request body should include a JSON of the [OrderRequest](./models.md#orderrequest) class.

## Example Request

```
POST /production/ssl/core/v1/order/subscription/subscr9836/get HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer eyJ0eXA..N9spaA
Content-Type: application/json
Content-Length: 158

{
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "challengeType": "DNS",
    "rootDomain": "shopeneur.com"
}
```

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Core API. An [Order](./models.md#order) entity to represent the certificate order is provided in the **body** of the response in JSON format.

# Example Response Body
```
{
    "status": "pending",
    "validationTokens": [
        {
            "tokenName": "_acme-challenge.www",
            "tokenValue": "hW9A7-hOZw1WQxLaxZbZRtrn5r3Tq9ufJ5IYxCODB3w",
            "challengeType": "DNS"
        }
    ],
    "challenges": [
        {
            "challengeType": "http-01",
            "status": "pending",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        },
        {
            "challengeType": "dns-01",
            "status": "pending",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        },
        {
            "challengeType": "tls-alpn-01",
            "status": "pending",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        }
    ],
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "certificateUri": null
}

```

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 404 Not Found

The order was not found.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.

