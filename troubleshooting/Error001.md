---
title: Error 001
description: Error 001
parent: Troubleshooting
nav_order: 2
---

# Error Code
Error 001

# Sample Error
Failed to create certificate with target Stand ALone for host : contoso.com for challenge : DNS. Could not validate contoso.com with challenge dns-01 for domain contoso.com, status reported : invalid. DNS problem: NXDOMAIN looking up TXT for _acme-challenge.contoso.com - check that a DNS record exists for this domain

# Target
- Stand Alone Certificates
- Stand ALone SAN Certificates

# Causes for the Error

- A DNS TXT record was not created in the domain registrar management portal to complete the DNS Challenge

- A domain does not exist for the hostname for which the certificate is being created for

# Solution

## Stand Alone Certificate

- Complete the [DNS Challenge](https://docs.rclapp.com/portal/stand-alone.html#completing-the-dns-challenge) for a Stand Alone Certificate

- Use the [Dig](https://docs.rclapp.com/portal/stand-alone.html#verifying-the-dns-txt-record-with-dig) site to verify the domain TXT record for a Stand Alone Certificate

## Stand Alone SAN Certificate

- Complete the [DNS Challenge](https://docs.rclapp.com/portal/stand-alone-san.html#completing-the-dns-challenge) for a Stand Alone SAN Certificate

- Use the [Dig](https://docs.rclapp.com/portal/stand-alone-san.html#verifying-the-dns-txt-record-with-dig) site to verify the domain TXT record for a Stand Alone SAN Certificate