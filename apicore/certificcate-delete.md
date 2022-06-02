---
title: Certificate Delete
description: RCL Core API - Delete a SSL/TLS certificate
parent: RCL Core API
nav_order: 9
---

# Certificate Delete
**V6.0.10**

The **Certificate Delete API** delate a SSL/TLS certificate.

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
https://rclapi.azure-api.net
```

# API Endpoint and Method

The endpoint for the **Certificate Delete** API is :

```
/production/ssl/core/v1/certificate/subscription/{subscriptionid}/delete
```

where the placeholder : {subscriptionid} is the **Subscription Id** of the user's subscription in the RCL Portal.

A ``DELETE`` request must be made to the endpoint.

# Request Parameter

The the name of the certificate must be included in a parameter named ``name`` in the request url.

## Example Request

```
DELETE /production/ssl/core/v1/certificate/subscription/sx-001/delete?name=www.shopeneur.com HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer eyJ0eXAiOi...ygSQ
```

# Response

## 200 Ok

This represents success in making an authorized request to the RCL Core API. The certificate has been successfully deleted.

## 401 Unauthorized

The authorization failed for the request. Check the body of the response for additional error details in ``text/plain`` format.

## 400 Bad Request

An error occurred while processing the request. Check the body of the response for additional error details in ``text/plain`` format.