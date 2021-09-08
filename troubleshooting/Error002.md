---
title: Error 002
description: Error 002
parent: Troubleshooting
nav_order: 3
---

# Error Code
Error 002

# Sample Error
Failed to create certificate with target Stand ALone for host : contoso.com for challenge : DNS. Could not validate contoso.com with challenge dns-01 for domain contoso.com, status reported : invalid. Incorrect TXT record "MMLJBtXCI62Lua06DJYZnZ1fvr5It7E28XelH8BKRdo" found at _acme-challenge.contoso.com

# Target
- Stand Alone Certificates
- Stand ALone SAN Certificates

# Causes for the Error

- A DNS TXT record was incorrectly added in the domain registrar management portal to complete the DNS Challenge

# Solution

## Stand Alone Certificate

- Add the correct DNS TXT record for [DNS Challenge](https://docs.rclapp.com/portal/stand-alone.html#completing-the-dns-challenge) for a Stand Alone Certificate

- Use the [Dig](https://docs.rclapp.com/portal/stand-alone.html#verifying-the-dns-txt-record-with-dig) site to verify the domain TXT record for a Stand Alone Certificate

## Stand Alone SAN Certificate

- Add the correct DNS TXT record for the [DNS Challenge](https://docs.rclapp.com/portal/stand-alone-san.html#completing-the-dns-challenge) for a Stand Alone SAN Certificate

- Use the [Dig](https://docs.rclapp.com/portal/stand-alone-san.html#verifying-the-dns-txt-record-with-dig) site to verify the domain TXT record for a Stand Alone SAN Certificate