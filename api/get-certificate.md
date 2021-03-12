---
title: GET Certificate
parent: API
nav_order: 3
---

# GET Certificate

The **Certificate API** will get a TLS/SSL certificate by its name (eg: contoso.com) from the **RCL Portal** user's subscription.

## Try it in the Developer's Portal

You can try out this API in the [RCL API Portal](https://letsencryptapi.developer.azure-api.net/) .

## Making the request

To make the request, follow these steps:

- Include an Access Token in the Authorization Header
- Make a GET request to the **Certificate** endpoint
- Include a parameter : ``name`` with the value set to the TLS/SSL certificate name 

### Certificate Endpoint

The API endpoint for the **Certificate API** is

```
https://letsencryptapi.azure-api.net/api/v2/Certificate
```

### Parameters

the following parameter is required for the **Certificate API** :

- name : the name of the certificate (eg: contoso.com)

### Access Token

An Access Token must be obtained to make the GET request. Include the token in the **Authorization** header as a **Bearer** token. 

Please follow the instructions in this link to obtain the Access Token:

- [Authorization: Obtaining an Access Token](./authorization)

### Example GET Request

```
GET /api/v2/Certificate?name=contoso.com HTTP/1.1
Host: letsencryptapi.azure-api.net
Authorization: Bearer eyJ0eXAiO ... 0X2tnSQLEANnSPHY0gKcgw
```

## Response

A successful response will indicate a **200 OK** status. A **CertificateResponse** object will be returned.

### CertificateResponse Object

| Property                   | Type          | Description                              |
| ---------------------------| ------------- |------------------------------------------|
| id                         | int           | id of the certificate                    |
| name                       | string        | name of the certificate                  |
| issueDate                  | string        | date the certificate was issued          |
| expiryDate                 | string        | expiry date of the certificate           |
| remoteCreateDate           | string        | date the certificate was saved in server |
| target                     | string        | creation option for the certificate      |
| renewal                    | string        | renewal type (Automatic or Manual)       |
| pemUri                     | string        | download link for .PEM certificate       |
| pfxUri                     | string        | download link for .PFX certificate       |
| crtUri                     | string        | download link for .CRT certificate       |
| cerUri                     | string        | download link for .CER certificate       |
| privateKeyUri              | string        | download link for .KEY private key       |
| certificateUri             | string        | download link for .CRT primary cert      |
| intermediateCertificateUri | string        | download link for .CRT ca bundle         |
| intermediateCertificateUri | string        | download link for .CRT full chain cert   |

### Sample Response

```json
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
```

- [Introduction to RCL API](./introduction)
- [Authorization: Obtaining an Access Token](./authorization)
- [GET CertificateList](./get-certificate-list)
- [POST CertificateRenewal](./post-certificate-renewal)
- [POST Certificate](./post-certificate)
- [Recommendations for Automation System Design](./automation-system)