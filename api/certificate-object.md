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
| orderUri            | string    | The URI to get details of an certificate order     | https:./acme  |
| subscriptionId      | int       | The id of the subscription that owns the certificate| 71           |
| tokens          | List of [ValidationToken](#validationtoken-object)    | A list of tokens to complete the challenge      |     |
| pfxString            | string    | The pfx certificate in string format                | MbRu7Evm..   |
| certificateDownloadUrl | [CertificateDownloadUrl](#certificatedownloadurl-object)    | An object that provides the url to download certificate and key|   |
| issueDate           | string    | The date the certificate was issued                 | 2024-12-03T23:52:13.4471564   |
| expiryDate          | string    | The date the certificate will expire                | 2024-12-03T23:52:13.4471564   |
| azureSubscriptionId | string    | The Azure Subscription Id that contains your resources (eg. DNS Zone)| 650085hg4... |
| accessToken         | string    | An Azure Access Token to access resources in your Azure subscription| eyJ0eXAiOiJKV1... |
| dnsZoneResourceGroup| string    | The Azure Resource Group that contains your Azure DNS Zone| myRG |

Notes

1. The root domain is the ‘apex’ domain. For instance, the root domain for the hostname: ‘shop.contoso.com’ is ‘contoso.com’. Similarly, the root domain for the hostname : ‘contoso.com’ is ‘contoso.com’ and ‘*.contoso.com’ is ‘contoso.com’.

2. In the 'http' challenge, you will place a file in the root of your website to prove that you control the domain. In the 'dns' challenge, you will place a TXT record in the in your Domain Registrar to prove that you control the domain.

3. The certificate type may include : 'Stand ALone', 'Azure DNS', 'Azure KeyVault + DNS' , 'Azure App Service'

# ValidationToken Object

The validation token object contains the token name and value to complete a 'http' or 'dns' challenge.

| Property            | Data Type | Description                                        |Example            |
| ------------------- | --------- |----------------------------------------------------|-------------------|
| tokenName           | string    | The name of the token                              | _acme-challenge   |
| tokenValue          | string    | The token value                                    | iuH5jstOQLXk2hGs  |
| challengeType       | string    | The challenge type, eg 'dns' or 'http'             | dns               |

# CertificateDownloadUrl Object

The certificate download url object will provide links to the certificate and its keys in various formats

| Property            | Data Type | Description                                         |Example           |
| ------------------- | --------- |-----------------------------------------------------|------------------|
| pemUrl              | string    | The url to download the certificate in 'pem' format | "https://...rf   |
| pfxUrl              | string    | The url to download the certificate in 'pfx' format | "https://...rf   |
| cerUrl              | string    | The url to download the certificate in 'cer' format | "https://...rf   |
| crtUrl              | string    | The url to download the certificate in 'crt' format | "https://...rf   |
| txtUrl              | string    | The url to download the certificate in 'txt' format | "https://...rf   |
| keyUrl              | string    | The url to download the private key in 'key' format | "https://...rf   |
| keyTxtUrl           | string    | The url to download the private key in 'txt' format | "https://...rf   |
| certCrtUrl          | string    | The url to download the primary certificate in 'crt' format | "https://...rf   |
| cabundleCrtUrl      | string    | The url to download the intermediate certificates in 'crt' format | "https://...rf|
| fullchainCrtUrl     | string    | The url to download the full chain certificate in 'crt' format | "https://...rf   |
