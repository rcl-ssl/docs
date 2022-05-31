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