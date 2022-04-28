---
title: Configure the Function
description: Configuring the RCL AutoRenew Function
parent: AutoRenew Function
nav_order: 3
---

# Configure the RCL AutoRenew Function App
**V6.0.10**

In this section, you will configure the [RCL AutoRenew Function](../autorenew/autorenew.md) app.

## Register an AAD Application

An Azure Active Directory (AAD) application must be registered to obtain permission to access a user's Azure resources (App Service, DNS Zone, Key Vault). Please refer to the following link for instructions on how to register the AAD application:

- [Registering an AAD Application](../authorization/aad-application)

## Set Access Control for the AAD application

Access control must be set for the AAD application to access resources in a user's Azure subscription. Please refer to the following link for instructions:

- [Setting Access Control for the AAD Application](../authorization/access-control-app)

## Get the AAD Credentials 

Please refer to the following link to get the AAD credentials to configure the function app :

- [Get the AAD Application Credentials](../authorization/aad-application#get-the-aad-application-credentials)

## Add the Configuration variables

- Open the function app and click on 'Configuration'

![install](../images/autorenew_configure/func.PNG)

Update the following configuration entries with the credentials from the AAD application :

- Auth:client_id - the AAD App Client Id
- Auth:client_secret - the AAD App Client Secret
- Auth:tenantId - the AAD App Tenant Id

![install](../images/autorenew_configure/func2.PNG)

- In the [RCL Portal](../portal/portal.md), open the 'Subscription Detials' page

![install](../images/autorenew_configure/add_subscriptionid.PNG)

- Scroll down and copy the 'Subscription Id' (Api:SubscriptionId) for configuration purposes

![install](../images/autorenew_configure/add_subscriptionid2.PNG)

- In the Function App configuration page, add the 'Subscription Id' value to the **Api:SubscriptionId** configuration entry

![install](../images/autorenew_configure/add_subscriptionid3.PNG)


- Click the 'Save' button when you are done

## Add the Client Id in the RCL Portal

The AAD Application must be registered in the [RCL Portal](../portal/portal.md) to associate the AAD application to a user's subscription.

The [RCL AutoRenew](../autorenew/autorenew.md) function app uses the RCL Public API to execute its operations.

To add the AAD Application's ``Client Id`` to the portal, please follow the instructions in this link :

- [Add the Client Id in the RCL Portal](https://docs.rclapp.com/api/authorization#add-the-client-id-in-the-rcl-portal)

## Next Step

- [Testing the AutoRenew Function](./test.md)



