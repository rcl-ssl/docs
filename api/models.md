---
title: API Models
description: The models for the RCL Public API
parent: RCL Renewal API
nav_order: 100
---

# Model Classes

This section contain the model classes for the RCL Renewal API.

# AuthToken

Represents an authorization token

| Parameter | Description | Type
| --- | --- |--- |
| access_token |The requested access token. | string |
| token_type |Indicates the token type value. | string |
| expires_in |How long the access token is valid (in seconds). | string |
| expires_on |The time when the access token expires. The date is represented as the number of seconds from 1970-01-01T0:0:0Z UTC until the expiration time. This value is used to determine the lifetime of cached tokens. | string |
| not_before |The time from which the access token becomes usable. The date is represented as the number of seconds from 1970-01-01T0:0:0Z UTC until time of validity for the token.| string |
| resource |The App ID URI of the receiving web service. The RCL resource. | string |

## Example

```
{
"access_token":"eyJ0eXAiO ....gKcgw",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://management.core.windows.net"
}
```

# ResourceRequest

Represents a request for a resource in the RCL Public API

| Parameter | Description | Type
| --- | --- |--- |
| accessToken |The Azure Resource Manager access token. | string |
| accessTokenKeyVault |The Key Vault access token. | string |

## Example
```
{
    "accessToken" : "eyJ0eXAiOiJk....ww",
    "accessTokenKeyVault" : "eyJ0eXAiOZ....DQ"
}
```

# Certificate

Represents a SSL/TLS certificate

| Parameter | Description | Type |
| --- | --- |--- |
| id |The id of the certificate. | int |
| certificateName |The name of the certificate. | string |
| rootDomain |The root domain for the certificate. | string |
| email |The email contact for the user creating the certificate. | string |
| challengeType |The challenge type to validate the certificate ('HTTP' or 'DNS'). | string |
| orderUri |The Lets Encrypt URI for the certificate order. | string |
| csrInfo |The Certificate Signing Request Information. | [CsrInfo](#csrinfo) |
| issueDate |The issue date of the certificate. | DateTime |
| expiryDate |The expiry date of the certificate. | DateTime |
| target |The certificate target type. | string |
| renewal |The certificate renewal ('Automatic' or 'Manual'). | string |
| subscriptionId |The subscription id of the account in the RCL Portal. | int |
| password |The password for the certificate. | string |
| pfxString |The string format of the PFX certificate. | string |
| azureSubscriptionId |The Azure subscription id of the user's azure account. | string |
| dnsZoneResourceGroup |The Azure DNS Zone resource group. | string |
| keyVaultName |The Azure Key Vault name. | string |
| keyVaultName |The Azure Key Vault Certificate Name. | string |
| siteId |An id to identify the Azure App Service site. | int |
| certificateDownloadUrl |The download urls for various certificate formats. | [CertificateDownloadUrl](#certificatedownloadurl) |

## Example

```
{
    "certificateName":"shopeneur.com",
    "rootDomain":null,
    "email":null,
    "challengeType":null,
    "orderUri":null,
    "csrInfo":null,
    "issueDate":"2022-05-10T03:31:32.2585666",
    "expiryDate":"2022-05-28T23:33:01.5479202",
    "target":"Azure Key Vault + DNS",
    "renewal":"Automatic",
    "id":3673,
    "subscriptionId":889,
    "password":null,
    "pfxString":null,
    "certificateDownloadUrl":null,
    "azureSubscriptionId":null,
    "dnsZoneResourceGroup":null,
    "keyVaultName":null,
    "keyVaultCertificateName":null,
    "siteId":0
}
```

# CsrInfo

Represents the Certificate Signing Request Information

| Parameter | Description | Type |
| --- | --- |--- |
| Id |The id of the csr info. | int |
| countryName |The name of the country. | string |
| locality |The city. | string |
| state |The state/region. | string |
| organization |The name of the organization. | string |
| organizationUnit |The unit of the organization. | string |
| subscriptionId |The subscription id of the account in the RCL Portal. | int |

# CertificateDownloadUrl

Represents the download URLs for various certificate formats

| Parameter | Description | Type |
| --- | --- |--- |
| pemUrl |The download url for the .PEM format. | string |
| pfxUrl |The download url for the .PFX format. | string |
| cerUrl |The download url for the .CER format. | string |
| crtUrl |The download url for the .CRT format. | string |
| txtUrl |The download url for the .TXT format. | string |
| keyUrl |The download url for the private key in .KEY format. | string |
| certCrtUrl |The download url for the Certificate in .CRT format. | string |
| cabundleCrtUrl |The download url for the Certificate Bundle in .CRT format. | string |
| fullchainCrtUrl |The download url for the Full Chain Certificate  in .CRT format. | string |

# CertificateRequest

Represents a request for a certificate operation

| Parameter | Description | Type
| --- | --- |--- |
| accessToken |The Azure Resource Manager access token. | string |
| accessTokenKeyVault |The Key Vault access token. | string |
| certificate |The SSL/TLS certificate. | [Certificate](#certificate) |

## Example

```
{
    "accessToken" : "eyJ0eXAiOiJk....ww",
    "accessTokenKeyVault" : "eyJ0eXAiOZ....DQ",
    "certificate" : {
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
}
```
