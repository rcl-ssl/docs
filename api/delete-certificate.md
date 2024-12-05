---
title: Delete Certificate
description: API for deleting a certificate
parent: API
nav_order: 7
---

# Delete a Certificate
**V8.0**

In this section, you will learn how to delete a certificate by its name.

## Prerequisites

Before you can use the API you must first :

- Obtain an [API Key](./authorization.md)
- Create the [CSR Information](../portal/csr-info.md)

## Authorization

Obtain the [API Key](./authorization.md) in the **Subscription > API Key** page in the RCL SSL Portal.

You must include the API Key in the authorization header of a request as a **Bearer Token**.

## API Endpoint

The endpoint for making API requests is :

- https://rclapi.azure-api.net

## Subscription

To make a request to the API, you must use your subscription. You can obtain the subscription value from the **Subscription > Details** page in the RCL SSL Portal.

![image](../images/api_authorization/subscription.png)

## DELETE request

Send a **DELETE** request to :

```bash
/prod/v3/ssl/certificate/subscription/{your-subscription}/delete/certificatename/{your-certificate-name}
```

### Example Request

```bash
DELETE /prod/v3/ssl/certificate/subscription/subscr-0000/delete/certificatename/shopeneur.com HTTP/1.1
Host: rclapi.azure-api.net
Authorization: Bearer resdfre-t435-dkjh-5re6
```

After you make the post request, a ```200 OK``` response will be returned. 

### Example Response

```bash
200 OK
```

## Error Handling

Errors in the API will be returned as plain text in the body of a response, usually with a ```400 Bad Request```

### Example Response

```bash
Certificate name is not defined.
```