---
title: Introducing the API
description: Using the RCL Core API to create and get SSL/TLS certificates
parent: RCL Core API
nav_order: 1
---

# Introduction
**V6.0.10**

The **RCL Core API** provides REST API services to:

- Create SSL/TLS certificates
- Get SSL/TLS certificates that were created 

## Primary Usage

Developers can use the APIs to build custom applications to create SSL/TLS certificates.

## Quick Start

Start using the RCL Core API in these simple steps :

- Step 1: [Obtain an Access Token](./authorization.md) to make authorized requests to the API

- Step 2: [Create a Certificate Order](./order-create.md) for a SSL/TLS certificate

- Step 3: [Get a Certificate Order](./order-get.md) for a SSL/TLS certificate

- Step 4: [Validate a Certificate Order](./order-validate.md) for a SSL/TLS certificate

- Step 5: [Finalize a Certificate Order](./order-finalize.md) for a SSL/TLS certificate

- Step 6: [Get a Certificate](./certificate-get.md)

- Step 7: [Get all Certificates](./certificate-get-all.md) in a subscription

- Step 8: [Delete a Certificate](./certificcate-delete.md)

## Rate Limits

The following rate limit is enforced for the API :

- Maximum of 100 requests per week for a subscriber

## Related Articles

- [Authorization: Obtaining an Access Token](./authorization.md)
