---
title: Introducing the API
description: Using the RCL API to get and renew certificates created in the RCL portal
parent: API
nav_order: 1
---

# Introduction

The **RCL API** provides free REST API services to:

- Get TLS/SSL certificates from an **RCL Portal** user's subscription
- Renew TLS/SSL certificates that are about to expire

## Primary Usage

Developers can use the APIs to build custom applications to automate the installation and renewal of certificates.

## Developer's Portal

Developers can explore and test the APIs in the **RCL Developers Portal** located at :

- [RCL Developer's Portal](https://letsencryptapi.developer.azure-api.net/)

## Quick Start

Start using the API in two simple steps.

[Obtain an Access Token](./authorization) to make authorized requests to the API.

Make an authorized request to any one of these endpoints:

- [GET Certificate](./get-certificate)
- [GET CertificateList](./get-certificate-list)
- [POST CertificateRenewal](./post-certificate-renewal)
- [POST Certificate](./post-certificate)

## Rate Limits

The following rate limit is enforced for the API :

- Maximum of 50 requests per week for a subscriber

## Related Articles

- [Authorization: Obtaining an Access Token](./authorization)
- [GET Certificate](./get-certificate)
- [GET CertificateList](./get-certificate-list)
- [POST CertificateRenewal](./post-certificate-renewal)
- [POST Certificate](./post-certificate-renewal)
- [Recommendations for Automation System Design](./automation-system)