---
title: Certificate Object
description: The Certificate Object is used to make requests to the RCL SSL API
parent: API
nav_order: 10
---

# Certificate Object

The certificate object is used to make requests to the RCL SSL API.

| Property            | Data Type | Description                                        |Example|
| ------------------- | --------- |----------------------------------------------------|---------------|
| certificateName     | string    | The hostname you are requesting the certificate for| contoso.com   |
| rootDomain          | string    | The root domain for the hostname <sup>1</sup>      | contoso.com   |
| challengeType       | string    | The challenge type, either 'http' or 'dns' <sup>2</sup>          | dns           |
| password            | string    | Set a password for the certificate                 | sgrtd$qwdd56  |
| target              | string    | The certificate type <sup>3</sup>                  | Stand ALone   |
| isSAN               | bool      | Whether the certificate is a SAN certificate       | false         |
| orderUri            | string    | The URI to get details of an certificate order     | https:.../acme/order/135518893/21015889444         |
| subscriptionId      | int       | The id of the subscription that owns the certificate| false         |
| tokens          | List<ValidationToken>    | The root domain for the hostname <sup>1</sup>      | contoso.com   |

Notes

1. The root domain is the ‘apex’ domain. For instance, the root domain for the hostname: ‘shop.contoso.com’ is ‘contoso.com’. Similarly, the root domain for the hostname : ‘contoso.com’ is ‘contoso.com’ and ‘*.contoso.com’ is ‘contoso.com’.

2. In the 'http' challenge, you will place a file in the root of your website to prove that you control the domain. In the 'dns' challenge, you will place a TXT record in the in your Domain Registrar to prove that you control the domain.

3. The certificate type may include : 'Stand ALone', 'Azure DNS', 'Azure KeyVault + DNS' , 'Azure App Service'

# ValidationToken Object

The validation token object contains the token name and value to complete a 'http' or 'dns' challenge.

| Property            | Data Type | Description                                        |Example|
| ------------------- | --------- |----------------------------------------------------|-------------------|
| tokenName           | string    | The name of the token                              | _acme-challenge   |
| tokenValue          | string    | The token value                                    | iuH5jstOQLXk2hGs  |
| challengeType       | string    | The challenge type, eg 'dns' or 'http'             | dns               |

