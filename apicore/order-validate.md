---
title: Order Validate
description: RCL Core API - Validate an order for a SSL/TLS certificate
parent: RCL Core API
nav_order: 5
---

# Order Validate 
**V6.0.10**

The **Order Validate API** will verify that you have control over (or own) the domain for which you are requesting the SSL/TLS certificate.

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

The endpoint for the **Order Validate** API is :

```
/production/ssl/core/v1/order/subscription/{subscriptionid}/validate
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the user's subscription in the RCL Portal.

A ``POST`` request must be made to the endpoint.

# Request Body

The request body should include a JSON of the [ValidationRequest](./models.md#validationrequest) class.

## Example Request

```
POST /production/ssl/core/v1/order/subscription/sx-001/validate HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer eyJ0eXAiOiJ...TKbWi7-d2Q
Content-Type: application/json

{
    "orderUri":"https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "challengeType":"DNS"
}
```

# Notes

- **DNS Validation** - To validate your domain with the ``DNS`` challenge, you will be required to create a DNS TXT record in your domain settings with your domain registrar. The name of the record should be the ``tokenName`` in the [ValidationToken](./models.md#validationtoken) of the [Order](./models.md#order). The value of the record should be the ``tokenValue`` in the [ValidationToken](./models.md#validationtoken) of the [Order](./models.md#order). For a SAN certificate, you will be required to place two(2) token values in the in a single DNS TXT record. This wll be represented by an array of two (2) ValidationTokens in the Order. The  array of ValidationTokens in the order will have the same ``tokenName``, but with two different ``tokenValues``.

## Example of a DNS ValidationToken Array a Certificate Order

```
"validationTokens": [
    {
        "tokenName": "_acme-challenge.www",
        "tokenValue": "hW9A7-hOZw1WQxLaxZbZRtrn5r3Tq9ufJ5IYxCODB3w",
        "challengeType": "DNS"
    }
]
```

## Example of a DNS ValidationToken Array for a SAN Certificate Order

```
Todo
```

- **HTTP Validation** - To validate your domain with the ``HTTP`` challenge, you will be required to place a file in the root of your website and ensure that this file can be accessed publicly on the web. The file must be an extensionless file with the name specified by the ``tokenName`` in the [ValidationToken](./models.md#validationtoken) of the [Order](./models.md#order). The contents of the file should be the ``tokenValue`` in the [ValidationToken](./models.md#validationtoken) of the [Order](./models.md#order). The file must be placed in a folder named: **.well-known/acme-challenge** (note the dot at the start) that must be created in the root of your website. For a SAN certificate, you will be required to place two files in the folder. This wll be represented by an array of two (2) ValidationTokens in the Order.

## Example of a HTTP ValidationToken Array for Certificate Order

```
Todo
```

## Example of a HTTP ValidationToken Array for SAN Certificate Order

```
Todo
```

- **Validated Order** - Once an Order is validated. You can [Get the Order](order-get.md) and view the status. The status of the order should be ``ready`` and the status of the challenge should be ``valid``. If an order validation has failed, you cannot try to re-validate the same order again. You will need to create a new [Certificate Order](./order-create.md) and validate this new order.

## Example of a ValidatedOrder
```
{
    "status": "ready",
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
    "certificateUri": null
}
```

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Core API. The certificate order was successfully validated.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.