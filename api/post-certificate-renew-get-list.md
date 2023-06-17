---
title: POST Certificate Renew Get List
description: RCL Renewal API - POST Certificate Renew Get List
parent: API
nav_order: 5
---

# POST Certificate Renew Get List 
**V6.0.10**

The **Certificate Renew Get List API** will return a list of certificates that will expire in the next 20 days.

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

The endpoint for the **POST Certificate Renew Get List** API is :

```
/v1/subscription/{subscriptionid}/public/certificate/renew/getlist
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the subscription in the RCL Portal.

# Request Body

The request body should include a JSON of the [ResourceRequest](./models.md#resourcerequest) class.

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Public API. An **Array** of [Certificate](./models.md#certificate) that are about to expire is provided in the **body** of the response in JSON format.

## 404 Notfound

If no certificates were found that matches the renewal criteria.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.

# Example Request

```
POST /public/v1/subscription/subscr-431/public/certificate/renew/getlist HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json

{
    "accessToken" : "eyJ0eXAiOiJk..ww",
    "accessTokenKeyVault" : "eyJ0eXAiOZ..DQ"
}
```

# Example Response Body
```
[
    {
        "certificateName": "shopeneur.com",
        "rootDomain": null,
        "email": null,
        "challengeType": null,
        "orderUri": null,
        "csrInfo": null,
        "issueDate": "2022-05-10T03:31:32.2585666",
        "expiryDate": "2022-05-28T23:33:01.5479202",
        "target": "Azure Key Vault + DNS",
        "renewal": "Automatic",
        "id": 3673,
        "subscriptionId": 889,
        "password": null,
        "pfxString": null,
        "certificateDownloadUrl": null,
        "azureSubscriptionId": null,
        "dnsZoneResourceGroup": null,
        "keyVaultName": null,
        "keyVaultCertificateName": null,
        "siteId": 0
    }
]

```



