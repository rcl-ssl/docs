---
title: Order Create
description: RCL Core API - Create and order for a SSL/TLS certificate
parent: RCL Core API
nav_order: 3
---

# Order Create 
**V6.0.10**

The **Order Create API** will create an order for a SSL/TLS certificate.

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
https://rclapi.azure-api.net/production/ssl/core
```

# API Endpoint and Method

The endpoint for the **Order Create** API is :

```
/v1/order/subscription/{subscriptionid}/create
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the user's subscription in the RCL Portal.

A POST request must be made to the endpoint

# Request Body

The request body should include a JSON of the [CertificateRequest](./models.md#resourcerequest) class.

## Example Request

```
{
  "hostName" : "shopeneur.com",
  "rootDomain" : "shopeneur.com",
  "email":"support@rclapp.com",
  "challengeType":"DNS",
  "isSAN":false
}
```

# Notes

- **hostName** - the hostName is the domain you are requesting the certificate for. Example, apex domain - contoso.com, sub domain - store.contoso.com, www sub domain www.contoso.com, wild card domain *.contoso.com

- **rootDomain** - the root domain is the ‘apex’ domain for the host name. For instance, the root domain for the hostname: ‘shop.contoso.com’ is ‘contoso.com’. Similarly, the root domain for the hostname : ‘contoso.com’ is also ‘contoso.com’

- **challengeType** - The challenge type used to validate your domain. To validate your domain with the ``HTTP`` challenge, you will be required to place a file in the root of your website and ensure that this file can be accessed publicly on the web. To validate your domain with the ``DNS`` challenge, you will be required to create a DNS TXT record in your domain settings with your domain registrar. The DNS challenge supports wildcard domains (*.contoso.com).

- **isSAN** - specify if the certificate is a SAN certificate. A Subject Alternative Name (SAN) SSL/TLS certificate will contain multiple domains in a single certificate. A SAN certificate created with the ``HTTP Challenge`` will contain the naked apex domain (e.g. contoso.com) and the www subdomain (e.g. www.contoso.com) in a single SSL/TLS certificate. A SAN certificate created with the ``DNS Challenge`` will contain the naked apex domain (e.g. contoso.com) and a wild card domain (e.g. \*.contoso.com) in a single SSL/TLS certificate. For a SAN certificate the hostName MUST be an apex domain (eg: contoso.com) AND the rootDomain MUST be the same as the hostName. Hostname must not include multiple domains, sub-domains, commas (,) and asterisk (*). 

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Core API. An [Order](./models.md#certificate) entity to represent the certificate order is provided in the **body** of the response in JSON format.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.

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