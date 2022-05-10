---
title: Introducing the API
description: Using the RCL API to get and renew certificates created in the RCL portal
parent: API
nav_order: 1
---

# Introduction
**V6.0.10**

The **RCL Public API** provides REST API services to:

- Get SSL/TLS certificates from an **RCL Portal** user's subscription
- Renew SSL/TLS certificates that are about to expire

## Primary Usage

Developers can use the APIs to build custom applications to automate the installation and renewal of SSL/TLS certificates.

## Quick Start

Start using the RCL Public API in two simple steps.

[Obtain Access Tokens](./authorization) to make authorized requests to the API.

Test authorized connectivity to the API

- [POST Certificate Test](./post-certificate-test.md)
- [POST Certificate Renew Get List](./post-certificate-renew-get-list.md)
- [POST Certificate Renew](./post-certificate.renew.md)

## Rate Limits

The following rate limit is enforced for the API :

- Maximum of 100 requests per week for a subscriber

## Related Articles

- [Authorization: Obtaining an Access Token](./authorization)
