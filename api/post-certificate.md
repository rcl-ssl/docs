---
title: POST Certificate 
description: RCL Renewal API - POST Certificate 
parent: API
nav_order: 4
---

# POST Certificate 
**V6.0.10**

The **Certificate API** will get a certificate by its name.

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
https://rclapi.azure-api.net/public
```

# API Endpoint

The endpoint for the **POST Certificate** API is :

```
/v1/subscription/{subscriptionid}/public/certificate
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the subscription in the RCL Portal.

# Request Body

The request body should include a JSON of the [CertificateRequest](./models.md#certificaterequest) class.

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Public API and returns a [Certificate](./models.md#certificate) in JSON format in the **body** of the response. 

## 404 Notfound

If the certificate was not found.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.

# Example Request

```
POST /public/v1/subscription/849/public/certificate HTTP/1.1
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

# Example Response Body

```
{
    "certificateName": "shopeneur.com",
    "rootDomain": "shopeneur.com",
    "email": "xxxx@mail.com",
    "challengeType": "DNS",
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/52..6/873..86",
    "csrInfo": null,
    "issueDate": "2022-05-10T03:31:32.2585666",
    "expiryDate": "2022-05-28T23:33:01.5479202",
    "target": "Azure Key Vault + DNS",
    "renewal": "Automatic",
    "id": 3673,
    "subscriptionId": 889,
    "password": "pwd1234",
    "pfxString": "MIACAQMw....5QCAgQAAAA=",
    "certificateDownloadUrl": {
        "pemUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..d168.pem",
        "pfxUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..d168.pfx",
        "cerUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168.cer",
        "crtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168.crt",
        "txtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168.certdownload.txt",
        "keyUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168.key",
        "certCrtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168-cert.crt",
        "cabundleCrtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168-cabundle.crt",
        "fullchainCrtUrl": "https://rclstrg.blob.core.windows.net/pem/cert/a6c..168-fullchain.crt"
    },
    "azureSubscriptionId": "97850..e5",
    "dnsZoneResourceGroup": "infrastructureRG",
    "keyVaultName": "rclkeyvault",
    "keyVaultCertificateName": "shopeneur-com",
    "siteId": 0
}
```