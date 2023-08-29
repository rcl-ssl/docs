---
title: GET Finalize Certificate Order
description: Finalize a certificate order from the Let's Encrypt V2 API using the RCL SSL Core API
parent: Core API
nav_order: 3
---

# GET Finalize Certificate Order
**V7.0.0**

The ``GET Finalize Certificate Order`` API will finalize a certificate order once the order has been successfully validated by completing the required ``HTTP`` or ``DNS`` challenge for the certificate.

Once the order is successfully finalized, a new certificate will be created and saved to the RCL SSL Portal. Any existing certificates with the same name will be replaced with the new certificate in the RCL SSL Portal. The API will return the certificate with links to download the certificate files to install in a web sever. 

This API is normally used when a certificate is the RCL SSL Portal it nearing its expiration date. Once a [Certificate Order](./get-certificate-order.md) is created for the certificate and the order is [Validated](), the order id **finalized** to create a new certificate to replace the expiring certificate.

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
The endpoint for the **GET Finalize Certificate Order** is :

```
/v1/subscription/{subscr_id}/core/certificate/{certificate_name}/finalize?orderuri={order_uri}
```

Replace the placeholders in the curly braces ``{}`` with the following:

| URI Parameters | Description |Type
| --- | --- |--- |
|subscr_id  | The ``Subcription Id`` of the user's subscription in the RCL SSL Portal |string|
|certificate_name  | The name of the certificate (Hostname) as displayed in the RCL SSL Portal | string |

| Query Parameters | Description |Type
| --- | --- |--- |
|order_uri  | The ``orderUri`` for the certificate order to be finalized |string|

# Response

## 200 Ok

This represents success in making an authorized request to the API and returns a [Certificate](./model.md#certificate) in JSON format in the **body** of the response. 

## 401 Unauthorized

The authorization failed for the API request. Check the body of the API response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the API request. Check the body of the API response for additional error details in ``text/plain`` format.

# Example API Request

```
GET /public/v1/subscription/sub_df45ghfh463nfhh/core/certificate/shopeneur.com/finalize?orderuri=https://acme-v02.api.letsencrypt.org/acme/order/116443104/10568102114 HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer 45ref546-67rf-65ytr-65tr-546trfred
```

# Example API Response Body

```json
{
    "certificateName": "shopeneur.com",
    "rootDomain": "shopeneur.com",
    "email": "support@rclapp.com",
    "challengeType": "DNS",
    "orderUri": "https://acme-staging-v02.api.letsencrypt.org/acme/order/116443104/10568102114",
    "issueDate": "2023-08-29T04:53:07.4476228",
    "expiryDate": "2023-11-27T04:53:07.4476827",
    "id": 342,
    "password": "pwd1234",
    "pfxString": "MIACAQMwgAYJKoZ...AgQAAAA=",
    "certificateDownloadUrl": {
        "pemUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d.pem",
        "pfxUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d.pfx",
        "cerUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d.cer",
        "crtUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d.crt",
        "txtUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d-certdownload.txt",
        "keyUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d.key",
        "keyTxtUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d.txt",
        "certCrtUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d-cert.crt",
        "cabundleCrtUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d-cabundle.crt",
        "fullchainCrtUrl": "https://path/bf0e9b01-a0cc-4a0e-b232-75265afd2c1d-fullchain.crt"
    }
}
```

