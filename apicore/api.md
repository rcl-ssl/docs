---
title: Core API
description: Using the RCL Core SSL API to get and renew certificates created in the RCL SSL portal
has_children: true
nav_order: 8
---

# RCL SSL Core API
**V7.0.0**

The RCL SSL Core API is used to programmatically renew certificates created in the **RCL SSL Portal**. 

# Scope

The RCL SSL Core API is used for certificates created with the following options:

- [Stand Alone](../portal/stand-alone.md)
- [Stand Alone SAN](../portal/stand-alone-san.md)

# Overview

The primary purpose of the API is to allow users of the RCL SSL Portal to build their own applications to automatically renew SSL/TLS certificates in their hosting environments.

# Suggested Strategy

## Step 1 : Identify Expiring Certificates

Use the [GET Certificate](./get-certificate.md) API to get a certificate by its name. You can check the certificate's expiry date to determine when it will expire. Your application can then identify which certificates should be renewed (say, 14 days before it expires). 

## Step 2 : Create a Certificate Order

For each certificate identified to be renewed, use the [GET Certificate Order](./get-certificate-order.md) API to create an order for a new certificate. In the API response , you will get the validations tokens to validate the certificate order and prove that you have control of your domain.

## Step 3 : Validate the Certificate Order

### HTTP Challenge

For the HTTP challenge, you are required to place a file in the root of your website. The file must be placed in a folder named : ``.well-known/acme-challenge``. This folder should be at the root of your website. The name of the file should be the ``tokenName`` of the validation token. It is an extension-less file. The content of the file should be the ``tokenValue``. You application should be able to programmatically place the file at the root of your website. The file must be publicly accessible on the web. For instance , you should be able to navigate to your website at ``http://your-domain/.well-known/acme-challenge/token-name`` and the token value should be displayed in the web browser. Let's Encrypt will check for this token value to pass the validation process.

For [SAN](../portal/stand-alone-san.md) certificates, you will need to place two files in the root of your website.


### DNS Challenge

For the DNS challenge, you must place a ``TXT Record`` in the management portal of your domain registrar. The domain registrar may provide an API to perform such a task. The name of the TXT Record should be the ``tokenName`` of the validation token. The value of the TXT Record should be the ``tokenValue``. Let's Encrypt will check for the DNS TXT Record to pass the validation.

For [SAN](../portal/stand-alone-san.md) certificates, you will need to place two values for the TXT Record.

## Step 4. Finalizing a Certificate Order

Once a certificate order was successfully validated , its status will change from ``pending`` to ``ready``. In the ready state, the certificate order should be **finalized** to create the actual SSL/TLS certificate. To finalize an order, use the [GET Finalize Certificate Order](./get-finalize-certificate-order.md) API. Once the certificate is finalized, links to the required certificate files to be installed in a web server will be returned in the API response.

## Step 5. Save the Certificate Files

Save the certificate files in a folder on your hosting machine where the web server can access. Ensure the folder has the necessary read/write permissions to access the certificate files. Configure the web server to use these files for SSL.

## Step 6. Run your Renewal Application on a schedule

Set your application to run steps 1 - 5 on a schedule, eg. once a week. This can be accomplished by using a Cron Job, Windows Service or Linux Daemon. The application will check for certificates to renew every week, renew certificates that are about to expire, validate and finalize the certificate order and save the certificate to a folder on your hosting machine.