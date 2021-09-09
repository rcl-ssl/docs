---
title: Error 003
description: Error 003
parent: Troubleshooting
nav_order: 4
---

# Error Code
Error 003

# Sample Error
Failed to create certificate with target Stand ALone for host : contoso.com for challenge : HTTP. Could not validate contoso.com with challenge http-01 for domain contoso.com, status reported : invalid. Invalid response from http://contoso.com/.well-known/acme-challenge/p85out_DYtVCyzoOpZLerAvtvtWr_R1gAKnQ3r9DAlQ

# Target
- Stand Alone Certificates
- Stand ALone SAN Certificates

# Causes for the Error

- The validation token was not added to the root of the website
- The validation token cannot be publicly accessed on the web

# Solution

## Stand Alone Certificate

- Add the [validation record](https://docs.rclapp.com/portal/stand-alone.html#completing-the-http-challenge) to the root of the website

- Ensure the [validation record](https://docs.rclapp.com/portal/stand-alone.html#completing-the-http-challenge) can be publicly accessed on the web

## Stand Alone SAN Certificate

- Add the [validation record(s)](https://docs.rclapp.com/portal/stand-alone-san.html#completing-the-http-challenge) to the root of the website

- Ensure the [validation record(s)](https://docs.rclapp.com/portal/stand-alone-san.html#completing-the-http-challenge) can be publicly accessed on the web