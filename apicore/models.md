---
title: API Models
description: The models for the RCL Core API
parent: RCL Core API
nav_order: 100
---

# Model Classes

This section contain the model classes for the RCL Core API.

# AuthToken

Represents an authorization token

| Parameter | Description | Type
| --- | --- |--- |
| access_token |The requested access token. | string |
| token_type |Indicates the token type value. | string |
| expires_in |How long the access token is valid (in seconds). | int |

## Example

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

# CertificateRequest

Represents a request for a SSL/TLS certificate

| Parameter | Description | Type
| --- | --- |--- |
| hostName |The host name for the certificate. | string |
| rootDomain |The root domain for the host name. | string |
| email |The email contact for the user requesting the certificate. | string |
| challengeType |The challenge type for validating the certificate. | string |
| isSAN |Whether the certificate is a SAN certificate. | bool |

## Example

```
{
    "hostName" : "www.shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "email":"support@mail.com",
    "challengeType":"DNS",
    "isSAN":false
}
```

# Order

Represents an order for a SSL/TLS certificate

| Parameter | Description | Type
| --- | --- |--- |
| status |The status of the order. | string |
| orderUri |The URI for the order. | string |
| certificateUri |The URI for the certificate. | string |
| validationTokens |The token to be used to validate the challenge for the order. | Array of [ValidationToken](#validationtoken) |
| challenges |The available challenges for the order. | Array of [Challenge](#challenge) |

## Example

```
{
    "status": "pending",
    "validationTokens": [
        {
            "tokenName": "_acme-challenge.www",
            "tokenValue": "hW9A7-hOZw1WQxLaxZbZRtrn5r3Tq9ufJ5IYxCODB3w",
            "challengeType": "DNS"
        }
    ],
    "challenges": [
        {
            "challengeType": "http-01",
            "status": "pending",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        },
        {
            "challengeType": "dns-01",
            "status": "pending",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        },
        {
            "challengeType": "tls-alpn-01",
            "status": "pending",
            "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
        }
    ],
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "certificateUri": null
}
```

# ValidationToken

Represents an token to be used to validate the SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| tokenName |The name of the token. | string |
| tokenValue |The value of the token. | string |
| challengeType |The challenge type for which this token must be used. | string |

## Example

```
{
    "tokenName": "_acme-challenge.www",
    "tokenValue": "hW9A7-hOZw1WQxLaxZbZRtrn5r3Tq9ufJ5IYxCODB3w",
    "challengeType": "DNS"
}
```

# Challenge

Represents a challenge that is used to validate the SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| challengeType |The type of the challenge. | string |
| status |The status of the challenge. | string |
| token |The base token for the challenge (may differ from the tokenValue). | string |

## Example

```
{
    "challengeType": "dns-01",
    "status": "pending",
    "token": "OavU5bQv41k5885ofozqxSJs5TgCulc4THtfdixGWdQ"
}
```

# OrderRequest

Represents a request to get a SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| orderUri |The URI of the order. | string |
| challengeType |The challenge type that was used to create the certificate order. | string |
| rootDomain |The root domain that was used to create the certificate order. | string |

## Example

```
{
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "challengeType": "DNS",
    "rootDomain": "shopeneur.com"
}
```

# ValidationRequest

Represents a request to validate a SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| orderUri |The URI of the order. | string |
| challengeType |The challenge type that was used to create the certificate order. | string |

## Example

```
{
    "orderUri": "https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "challengeType": "DNS"
}
```

# FinalizationRequest

Represents a request to validate a SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| hostName |The host name for the certificate. | string |
| rootDomain |The root domain for the host name. | string |
| orderUri |The URI of the order. | string |
| challengeType |The challenge type that was used to create the certificate order. | string |
| email |The email contact for the user requesting the certificate. | string |
| password |The password for the certificate. | string |
| csrInfo |The password for the certificate. | [CsrInfo](#csrinfo) |

## Example

```
{
    "hostName":"www.shopeneur.com",
    "rootDomain":"shopeneur.com",
    "orderUri":"https://acme-v02.api.letsencrypt.org/acme/order/527702946/93863252796",
    "challengeType":"DNS",
    "email":"support@mail.com",
    "password":"pwd1234",
    "csrInfo":{
        "countryName":"Trinidad",
        "locality":"Homeland Gardens",
        "state":"Cunupia",
        "organization":"Ray Consulting Limited",
        "organizationUnit":"IT"
    }
}
```

# CsrInfo

Represents the information of the organization requesting the SSL/TLS certificate

| Parameter | Description | Type
| --- | --- |--- |
| countryName |The country. | string |
| locality |The city. | string |
| state |The State/Region. | string |
| organization |The organization name. | string |
| organizationUnit |The organization department or unit. | string |

## Example

```
{
    "countryName":"Trinidad",
    "locality":"Homeland Gardens",
    "state":"Cunupia",
    "organization":"Ray Consulting Limited",
    "organizationUnit":"IT"
}
```

