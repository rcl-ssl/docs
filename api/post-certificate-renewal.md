---
title: POST Certificate Renewal
description: RCL API - POST Certificate Renewal
parent: API
nav_order: 5
---

# POST Certificate Renewal

The **Certificate Renewal API** schedules TLS/SSL certificates for renewal in a user's subscription from the **RCL Portal**. 

## Try it in the Developer's Portal

You can try out this API in the [RCL API Portal](https://letsencryptapi.developer.azure-api.net/) .

The result of the renewal process can be obtained from the portal in the 'Notification' page after the certificates have been actually renewed. If a certificate fails to renew, an email will be sent to the user alerting that a certificate renewal failure occurred for the identified certificate.

## Making the request

To make the request, follow these steps:

- Include an Access Token in the Authorization Header
- Make a POST request to the **Certificate Renewal** endpoint
- Include an AccessTokenPayload in the body of the POST request if certificates were created for Azure Key Vault (**the post body can be blank if there are no Azure Key Vault certificates**)

### Certificate Renewal Endpoint

The API endpoint for the **Certificate Renewal API** is

```
https://letsencryptapi.azure-api.net/api/v2/CertificateRenewal
```

### Access Token

Obtain an Access Token to make the request. Include the token in the **Authorization** header as a **Bearer** token. 

Please follow the instructions in this link to obtain the Access Token:

- [Authorization: Obtaining and Access Token](./authorization)

### Example POST Request (Excluding AccessTokenPayload object)

```
POST /api/v2/CertificateRenewal HTTP/1.1
Host: letsencryptapi.azure-api.net
Authorization: Bearer eyJ0eXAiO ... 0X2tnSQLEANnSPHY0gKcgw
```

### Example POST Request (Including AccessTokenPayload object)

```
POST /api/v2/CertificateRenewal HTTP/1.1
Host: letsencryptapi.azure-api.net
Authorization: Bearer eyJ0eXAiO ... 0X2tnSQLEANnSPHY0gKcgw
Content-Type: application/json

{
    "keyVaultAccessToken" : "ejbrestvd123_...."
}
```

An Access Token for Azure Key Vault can be obtained by making a POST request to the AD token endpoint specifying the following value for the ``resource`` property : https://vault.azure.net

 ```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fvault.azure.net
 ```
Read this link for more information on obtaining Access Tokens:

[Authorization: Obtaining an Access Token](./authorization)

## Response

A successful response will indicate a **200 OK** status. If certificates were found that need to be renewed, an array of [CertificateResponse](./get-certificate#certificateresponse-object) objects will be returned representing the certificates that were **scheduled for renewal**.

### Sample Response

```json
[
    {
        "id":158,
        "name":"contoso.com",
        "issueDate":"2021-01-30T01:04:32.1430009",
        "expiryDate":"2021-04-30T01:04:32.1430019",
        "remoteCreateDate":"",
        "target":"Azure DNS",
        "renewal":"Automatic",
        "pemUri":"",
        "pfxUri":"",
        "crtUri":"",
        "cerUri":"",
        "privateKeyUri":"",
        "certificateUri":"",
        "intermediateCertificateUri":"",
        "fullChainCertificateUri":""
    }
]
```

If no certificates were found that require renewal, the API will return an empty array.

```
[]
```

**Note: the API will return the certificates that were scheduled for renewal. To get the certificates that were actually renewed, you should wait a few minutes and then make a GET request to the [Certificate List API](./get-certificate-list) and make a determination as to which certificates were renewed.**

## Related Articles

- [Introduction to RCL API](./introduction)
- [Authorization: Obtaining an Access Token](./authorization)
- [GET CertificateList](./get-certificate-list)
- [POST Certificate](./post-certificate)
- [Recommendations for Automation System Design](./automation-system)
