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
| expires_in |How long the access token is valid (in seconds). | string |

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
| email |The challenge type for validating the certificate. | string |
| isSAN |Whether the certificate is a SAN certificate. | bool |

## Example

```
{
  "hostName" : "shopeneur.com",
  "rootDomain" : "shopeneur.com",
  "email":"support@rclapp.com",
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
  "hostName" : "shopeneur.com",
  "rootDomain" : "shopeneur.com",
  "email":"support@rclapp.com",
  "challengeType":"DNS",
  "isSAN":false
}
```

# ValidationToken

Represents an token to be used to validate the SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| tokenName |The name of the token. | string |
| tokenValue |The value of the token. | string |
| challengeType |The challenge type for which this token must be used. | string |

# Challenge

Represents a challenge thst is used to validate the SSL/TLS certificate order

| Parameter | Description | Type
| --- | --- |--- |
| challengeType |The type of the challenge. | string |
| status |The status of the challenge. | string |
| token |The base token for the challenge (may differ from the tokenValue). | string |