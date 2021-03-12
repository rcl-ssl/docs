---
title: Installation
parent: AutoRenew Function
nav_order: 2
---

# Installing AutoRenew Function

In this section, you will learn how to install the **RCL Auto Renew Function** in an Azure account.

## Install in Azure

- Open the [Github Project Page ](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.AutoRenew) for the AutoRenew function , and in the **master** branch, click on the 'Deploy to Azure' button on the **README** page

![install](../images/autorenew_installation/azure_deploy.PNG)

- Create a new **Resource Group** and install the function app. Do not edit the 'Auto' settings.

![install](../images/autorenew_installation/azure_deploy2.PNG)

The following Azure applications will be installed in the Resource Group :

- Function app - this is used to automatically renew the TLS/SSL certificates
- Consumption plan - the function app will run on a [consumption plan](https://docs.microsoft.com/en-us/azure/azure-functions/consumption-plan) and the user will pay only when the function is running
- Storage account - required by the function app

The estimated cost for these Azure resources may be a few cents or dollars per month based on the number of certificates in a user's subscription.

![install](../images/autorenew_installation/azure_deploy3.PNG)

## Next Steps

- [Configuring AutoRenew Function](./configure.md)
- [Testing AutoRenew Function](./test.md)