---
title: Stand Alone
description: API for ordering and creating a Stand Alone Certificate
parent: API
nav_order: 4
---

# Stand Alone Certificate
**V8.0**

In this section, you will learn how to order and create a [Stand Alone Certificate](../portal/stand-alone.md) (including [SAN](../portal/stand-alone-san.md)) using the [RCL SSL API](./api.md).

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

## Create a Certificate Order

You will first need to create a certificate order before you can create a certificate.

Send a **POST** request to :

```bash
/prod/v3/ssl/certificate/subscription/{your-subscription}/order/create
```

Include a [Certificate object](./certificate-object.md) in the body of the request in jSON format. The following example shows the required fields for the object.

```json
{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Stand ALone",
    "isSAN": false
}

```

### Example Request

```bash
POST /prod/v3/ssl/certificate/subscription/subscr-0000/order/create HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json
Authorization: Bearer resdfre-t435-dkjh-5re6
Content-Length: 229

{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Stand ALone",
    "isSAN": false
}
```

### Example Response
```json
{
    "certificateName": "shopeneur.com",
    "rootDomain": "shopeneur.com",
    "email": "rcl@mail.com",
    "challengeType": "dns",
    "orderUri": "https://acme-staging-v02.api.letsencrypt.org/acme/order/135518893/21014318564",
    "target": "Stand ALone",
    "subscriptionId": 71,
    "password": "password123",
    "tokens": [
        {
            "tokenName": "_acme-challenge",
            "tokenValue": "RNUMtaXCdx0KGMneUmlP_DJzg7sew9e8FFOjsfoNNb8",
            "challengeType": "DNS",
            "domain": "shopeneur.com"
        }
    ]
}
```

## Create a Certificate

Once an order is created for a certificate, you will need to validate that you own or control the domain that 
you are requesting the certificate for.

To [validate the http challenge](../portal/stand-alone.md#completing-the-http-challenge) you will need to place 
a file at the root of your website.

To [validate the dns challenge](../portal/stand-alone.md#completing-the-dns-challenge) you will need to add 
a TXT record in your DNS Registrar.

Once you complete the validation, you can now send a request to create a certificate.

Send a **POST** request to :

```bash
/prod/v3ssl/certificate/subscription/{your-subscription}/schedule/create
```

Include a [Certificate object](./certificate-object.md) in the body of the request in jSON format. The following example shows the required fields for the object.

```json
{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Stand ALone",
    "isSAN": false,
    "orderUri": "https://acme-staging-v02.api.letsencrypt.org/acme/order/135518893/21014318564"
}

```

You must include the Order Uri in the Certificate object.

### Example Request

```bash
POST /prod/v3/ssl/certificate/subscription/subscr-0000/schedule/create HTTP/1.1
Host: rclapi.azure-api.net
Content-Type: application/json
Authorization: Bearer resdfre-t435-dkjh-5re6
Content-Length: 296

{
    "certificateName" : "shopeneur.com",
    "rootDomain" : "shopeneur.com",
    "challengeType" : "dns",
    "email" : "rcl@mail.com",
    "password" : "password123",
    "target": "Stand ALone",
    "isSAN": false,
    "orderUri":"https://acme-staging-v02.api.letsencrypt.org/acme/order/135518893/20709585374"
}
```
After you make the post request, a ```200 OK``` response will be returned. 

### Example Response

```bash
200 OK
```

Your certificate will then be scheduled for creation at a later time. During this process, your domain will be validated based on the challenge you completed.
Once the domain is validated, your certificate will be created.

You can access your new certificate using the [Get Certificate API](get-certificate.md)
