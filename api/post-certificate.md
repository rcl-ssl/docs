---
title: POST Certificate
parent: API
nav_order: 6
---

# POST Certificate

The **Certificate API** will update a TLS/SSL certificate from the **RCL Portal** to flag that the certificate was installed in the remote web server. This operation should be executed after a certificate is downloaded and saved on the web server.

## Try it in the Developer's Portal

You can try out this API in the [RCL API Portal](https://letsencryptapi.developer.azure-api.net/) .

## Making the request

To make the request, follow these steps:

- Include an Access Token in the Authorization Header
- Make a POST request to the **Certificate** endpoint
- Include a [CertificateResponse](./get-certificate#certificateresponse-object) object as a JSON in the body of the POST request

## Certificate Endpoint

The API endpoint for the **Certificate API** is

```
https://letsencryptapi.azure-api.net/api/v2/Certificate
```

## Request Payload

A JSON representation of the [CertificateResponse](./get-certificate#certificateresponse-object) object must be sent in the body of the POST request. The properties : ``remoteCreateDate``, ``id``, ``name`` must be included in the CertificateResponse object to indicate the date that the certificate was downloaded and saved in the server.

### Access Token

Obtain an Access Token to make the request. Include the token in the **Authorization** header as a **Bearer** token. 

Please follow the instructions in this link to obtain the Access Token:

- [Authorization: Obtaining an Access Token](./authorization)

### Example POST Request

```
POST /api/v2/Certificate HTTP/1.1
Host: letsencryptapi.azure-api.net
Authorization: Bearer eyJ0eXAiO ... 0X2tnSQLEANnSPHY0gKcgw
Content-Type: application/json


{
    "id":158,
    "name":"contoso.com",
    "remoteCreateDate":"2021-01-30T01:04:32"
}
```

## Response

A successful response will indicate a **200 OK** status. A [CertificateResponse](./get-certificate#certificateresponse-object) object will be returned containing the properties : ``remoteCreateDate``, ``id``, ``name``.

### Sample Response

```json
[
    {
        "id":158,
        "name":"contoso.com",
        "remoteCreateDate":"2021-01-30T01:04:32"
    }
]
```

## Related Articles

- [Introduction to RCL API](./introduction)
- [Authorization: Obtaining an Access Token](./authorization)
- [GET Certificate](./get-certificate)
- [GET CertificateList](./get-certificate-list)
- [POST CertificateRenewal](./post-certificate-renewal)
- [Recommendations for Automation System Design](./automation-system)