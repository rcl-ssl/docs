---
title: GET Certificate
description: Get a certificate from the RCL SSL Portal using the RCL SSL Core API
parent: Core API
nav_order: 3
---

# GET Certificate 
**V7.0.0**

The ``GET Certificate`` API will return a certificate by its name from the RCL SSL Portal.

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
/public/v1/subscription/{subscr_id}/core/certificate/{certificate_name}
```

Replace the placeholders in the curly braces ``{}`` with the following:

| Parameter | Description |Type
| --- | --- |--- |
|subscr_id  | The ``Subcription Id`` of the user's subscription in the RCL SSL Portal |string|
|certificate_name  | The name of the certificate (Hostname) as displayed in the RCL SSL Portal | string |

# Response

## 200 Ok

This represents success in making an authorized request to the API and returns a [Certificate](./models.md#certificate) in JSON format in the **body** of the response. 

## 401 Unauthorized

The authorization failed for the API request. Check the body of the API response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the API request. Check the body of the API response for additional error details in ``text/plain`` format.

# Example API Request

```
GET /public/v1/subscription/sub_df45ghfh463nfhh/core/certificate/shopeneur.com HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer 45ref546-67rf-65ytr-65tr-546trfred
```

# Example API Response Body

```json
{
    "certificateName": "shopeneur.com",
    "rootDomain": "shopeneur.com",
    "email": "support@mail.com",
    "challengeType": "DNS",
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/116443104/10561456874",
    "issueDate": "2023-08-28T16:54:45.7728501",
    "expiryDate": "2023-11-26T16:54:45.7729979",
    "id": 341,
    "password": "pwd1234",
    "pfxString": "MIACAQ..SwQUa6VcuNGqfAd9OKA7LC2PjJGFH+oCAgQAAAA=",
    "certificateDownloadUrl": {
        "pemUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4.pem",
        "pfxUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4.pfx",
        "cerUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4.cer",
        "crtUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4.crt",
        "txtUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4-certdownload.txt",
        "keyUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4.key",
        "keyTxtUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4.txt",
        "certCrtUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4-cert.crt",
        "cabundleCrtUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4-cabundle.crt",
        "fullchainCrtUrl": "https://path/153c904c-0832-4381-bbf9-20f2324ce8f4-fullchain.crt"
    }
}
```


