---
title: GET Certificate List
parent: API
nav_order: 4
---

# GET Certificate List

The **Certificate List API** will get a list of TLS/SSL certificates in a user's subscription from the **RCL Portal**.

## Try it in the Developer's Portal

You can try out this API in the [RCL API Portal](https://letsencryptapi.developer.azure-api.net/) .

## Making the request

To make the request, follow these steps:

- Include an Access Token in the Authorization Header
- Make a GET request to the **Certificate List** endpoint

### Certificate List Endpoint

The API endpoint for the **Certificate List API** is

```
https://letsencryptapi.azure-api.net/api/v2/CertificateList
```

### Access Token

Obtain an Access Token to make the request. Include the token in the **Authorization** header as a **Bearer** token. 

Please follow the instructions in this link to obtain the Access Token:

- [Authorization: Obtaining and Access Token](./authorization)

### Example GET Request

```
GET /api/v2/CertificateList HTTP/1.1
Host: letsencryptapi.azure-api.net
Authorization: Bearer eyJ0eXAiO ... 0X2tnSQLEANnSPHY0gKcgw
```

## Response

A successful response will indicate a **200 OK** status. An array of [CertificateResponse](./get-certificate#certificateresponse-object) objects will be returned.

### Sample Response

```json
[
    {
        "id":158,
        "name":"contoso.com",
        "issueDate":"2021-01-30T01:04:32.1430009",
        "expiryDate":"2021-04-30T01:04:32.1430019",
        "remoteCreateDate":"2021-01-30T00:00:00",
        "target":"Azure DNS",
        "renewal":"Automatic",
        "pemUri":"https://azure-storage/pem",
        "pfxUri":"https://azure-storage/pfx",
        "crtUri":"https://azure-storage/crt",
        "cerUri":"https://azure-storage/cer",
        "privateKeyUri":"https://azure-storage/pvtkey",
        "certificateUri":"https://azure-storage/cert",
        "intermediateCertificateUri":"https://azure-storage/ca",
        "fullChainCertificateUri":"https://azure-storage/full"
    }
]
```

- [Introduction to RCL API](./introduction)
- [Authorization: Obtaining an Access Token](./authorization)
- [GET Certificate](./get-certificate)
- [POST CertificateRenewal](./post-certificate-renewal)
- [POST Certificate](./post-certificate)
- [Recommendations for Automation System Design](./automation-system)

