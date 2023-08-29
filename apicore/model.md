---
title: Models
description: The models for the RCL SSL Core API
parent: Core API
nav_order: 100
---

# Model Classes

This section contain the model classes for the RCL SSL Core API.

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
| issueDate |The issue date of the certificate. | DateTime |
| expiryDate |The expiry date of the certificate. | DateTime |
| password |The password for the certificate. | string |
| pfxString |The string format of the PFX certificate. | string |
| certificateDownloadUrl |The download urls for various certificate formats. | [CertificateDownloadUrl](#certificatedownloadurl) |

## Example

```
{
    "certificateName":"shopeneur.com",
    "rootDomain":null,
    "email":null,
    "challengeType":null,
    "orderUri":null,
    "issueDate":"2022-05-10T03:31:32.2585666",
    "expiryDate":"2022-05-28T23:33:01.5479202",
    "password":null,
    "pfxString":null,
    "certificateDownloadUrl":null
}
```

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

# Order

Represents a SSL/TLS certificate order

| Parameter | Description | Type |
| --- | --- |--- |
| status |The status of the order (``pending``, ``ready`` or ``invalid``). | string |
| validationTokens |An array of [ValidationToken](./model.md#validationtoken) required to validate the order (prove ownership of the domain). | string |
| orderUri |The URI or the order in Let's Encrypt. | string |
| certificateUri |The URI to download the certificate from Let's Encrypt. | string |

# ValidationToken

Represents a token to validate (prove ownership of a domain) a certificate order

| Parameter | Description | Type |
| --- | --- |--- |
| tokenName |The name of the token. For a DNS Challenge, it will be the ``TXT record`` to place in the the DNS provider. For the HTTP Challenge, it is the ``folder name`` to place at the root of the website  | string |
| tokenValue |The value of the token. For a DNS Challenge, it will be the ``value`` of the TXT record to place in the the DNS provider. For the HTTP Challenge, it is the ``value`` to place at the root folder of the website  | string |
| challengeType |The Challenge Type for the validation (``DNS`` or ``HTTP``)  | string |
| domain |The domain (certificate name or Hostname) for which the certificate is sought | string |