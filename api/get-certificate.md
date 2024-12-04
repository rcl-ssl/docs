---
title: Get Certificate
description: API to get a certificate by its name
parent: API
nav_order: 3
---

# Get a Certificate
**V8.0**

In this section, you will learn how to order and get a certificate by its name.

## Prerequisites

Before you can use the API you must first :

- Obtain an [API Key](./authorization.md)
- Create the [CSR Information](../portal/csr-info.md)

## Authorization

Obtain the [API Key](./authorization.md) in the **Subscription > API Key** page in the RCL SSL Portal.

You must include the API Key in the authorization header of a request as a **Bearer Token**.


## API Endpoint

The endpoint for making API requests is :

- https://rclapi.azure-api.net/prod/v3

## Subscription

To make a request to the API, you must use your subscription. You can obtain the subscription value from the **Subscription > Details** page in the RCL SSL Portal.

![image](../images/api_authorization/subscription.png)

## GET request

Send a **GET** request to :

```bash
ssl/certificate/subscription/{your-subscription}/get/certificatename/{your-certificate-name}
```

### Example Request

```bash
GET /prod/v3/ssl/certificate/subscription/subscr-0000/get/certificatename/shopeneur.com HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer resdfre-t435-dkjh-5re6
```

### Example Response

```json
{
    "certificateName": "shopeneur.com",
    "rootDomain": "shopeneur.com",
    "email": "rcl@mail.com",
    "challengeType": "dns",
    "orderUri": "https://acme-staging-v02.api.letsencrypt.org/acme/order/135518893/21014318564",
    "issueDate": "2024-12-03T23:52:13.4471564",
    "expiryDate": "2025-03-03T23:52:13.4471907",
    "target": "Stand ALone",
    "id": 451,
    "subscriptionId": 71,
    "password": "password123",
    "pfxString": "MbRu7Evm....",
    "certificateDownloadUrl": {
        "pemUrl": "https://...rfTdROqr2VQhNtTjt09rHlVK%2Fys%3D",
        "pfxUrl": "https://...N9TBGaOJxXDAjdX6PBhGd5lZ0%2Fw%3D",
        "cerUrl": "https://...BAr28qXUUN9XfYOG8i8oWoTLgFL3VU%3D",
        "crtUrl": "https://...BxU09ngdJgGilUflCT0%3D",
        "txtUrl": "https://...vCbWvBimqoWmyPOofpgaU%3D",
        "keyUrl": "https://...pDB1R8RskVJwy%2B4FxLIQOMbi0%3D",
        "keyTxtUrl": "https://...F6EupP%2B%2BznBH4lwk%3D",
        "certCrtUrl": "https://...gWOXQRJPD7OcNjyrx%2FYDC9Ur40I%3D",
        "cabundleCrtUrl": "https://...M2LGkSa8%2B73lxKoPM9owdBdRQSwC4IXyM%3D",
        "fullchainCrtUrl": "https://...3xwTwWG%2B58dksa82onEbVWwX8c%3D"
    }
}
```


