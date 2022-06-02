---
title: Order Finalize
description: RCL Core API - Finalize an order for a SSL/TLS certificate
parent: RCL Core API
nav_order: 6
---

# Order Finalize
**V6.0.10**

The **Order Finalize API** creates a SSL/TLS certificate after a certificate order has been [validated](./order-validate.md).

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

The endpoint for the **Order Finalize** API is :

```
/production/ssl/core/v1/order/subscription/{subscriptionid}/finalize
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the user's subscription in the RCL Portal.

A ``POST`` request must be made to the endpoint. The order must be have a ``ready`` status before it can be finalized.

# Request Body

The request body should include a JSON of the [FinalizationRequest](./models.md#finalizationrequest) class.

## Example Request

```
POST /production/ssl/core/v1/order/subscription/subscr9836/finalize HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer eyJ0eXAiOiJKV1Q..O4J411Fzg
Content-Type: application/json

{
    "hostName":"www.shopeneur.com",
    "rootDomain":"shopeneur.com",
    "orderUri":"https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "challengeType":"DNS",
    "email":"support@mail.com",
    "password":"pwd1234",
    "csrInfo":{
        "countryName":"Trinidad",
        "locality":"Homeland Gardens",
        "state":"Cunupia",
        "organization":"Ray Consulting Limited",
        "organizationUnit":"IT"
    }
}
```

# Notes

- **Certificate Order Status** - before an order can be finalized, the order status must be in the ``ready`` state 

- **Finalized Order** - when an order is finalized a certificate will be created and stored for retreival. You can then use the relevant API to get the certificates. The status of the order will be set to ``valid`` for a finalized order. You should not try to re-finalize an order in the ``valid`` state.

## Example of a Finalized Order
```
{
    "status": "valid",
    "validationTokens": [
        {
            "tokenName": "_acme-challenge.www",
            "tokenValue": "hW9A7-hOZw1WQxLaxZbZRtrn5r3Tq9ufJ5IYxCODB3w",
            "challengeType": "DNS"
        }
    ],
    "challenges": [
        {
            "challengeType": "dns-01",
            "status": "valid",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        }
    ],
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "certificateUri": "https://acme-v02.api.letsencrypt.org/acme/cert/04458562681165e50f2db2f40239967ccf85"
}
```

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Core API. The certificate order was successfully finalized.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.