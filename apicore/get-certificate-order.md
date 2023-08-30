---
title: GET Certificate Order
description: Get a certificate order from the Let's Encrypt V2 API using the RCL SSL Core API
parent: Core API
nav_order: 4
---

# GET Certificate Order
**V7.0.0**

The ``GET Certificate Order`` API will create an order for a certificate by its name from the Let's Encrypt V2 API. The order will be created using the properties of the certificate in the RCL SSL Portal.

This API is normally used when a certificate in the RCL SSL Portal it nearing its expiration date. A certificate order is created for the certificate with the intention of finalizing the order to create a new certificate to replace the expiring certificate.

# Authorization

An **Api Key** must be used to make authorized API requests. Please follow the instructions in the link below to acquire the key :

[Get an Api Key](./authorization.md)

The Api Key must be placed in the ``Authorization`` header of the API request as a ``Bearer`` token.

Example :
```
Authorization: Bearer 45ref546-67rf-65ytr-65tr-546trfred
```

# Subscription Id

Each request to the API must include the **Subscription Id** of the user's subscription in the RCL SSL Portal as a parameter in the API request url.

Please follow the instructions in the link below to get the ``Subscription Id`` :

[Get the Subscription Id](subscription-id.md)

# Base URI

The base URI for the RCL SSL Core API is :
```
https://rclapi.azure-api.net
```

# API Request

## API Method

``GET``

## Endpoint 
The endpoint for the **GET Certificate** is :

```
/v1/subscription/{subscr_id}/core/certificate/{certificate_name}/order
```

Replace the placeholders in the curly braces ``{}`` with the following:

| Parameter | Description |Type
| --- | --- |--- |
|subscr_id  | The ``Subcription Id`` of the user's subscription in the RCL SSL Portal |string|
|certificate_name  | The name of the certificate (Hostname) as displayed in the RCL SSL Portal | string |

# Response

## 200 Ok

This represents success in making an authorized request to the API and returns an [Order](./model.md#order) in JSON format in the **body** of the response. 

## 401 Unauthorized

The authorization failed for the API request. Check the body of the API response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the API request. Check the body of the API response for additional error details in ``text/plain`` format.

# Example API Request

```
GET /public/v1/subscription/sub_df45ghfh463nfhh/core/certificate/shopeneur.com/order HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer 45ref546-67rf-65ytr-65tr-546trfred
```

# Example API Response Body

```json
{
    "status": "pending",
    "validationTokens": [
        {
            "tokenName": "_acme-challenge",
            "tokenValue": "pder_53er44PhE-keudgge45630",
            "challengeType": "DNS",
            "domain": "shopeneur.com"
        }
    ],
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/116443104/10567267084",
    "certificateUri": null
}
```