---
title: Users
parent: Authorization
nav_order: 6
---

# Users

A user must be assigned to a subscription to use the subscription. When a subscription is created, the person creating the subscription is called the 'purchaser'. For a single subscription, the purchaser is automatically assigned as a 'user' in the subscription to use the application.

If a 'purchaser' creates another subscription, no user is assigned to the subscription. The purchaser must teh manually assign a user to use the subscription.

## Assign a User to a Subscription

- Open Subscription > Users
- Click on the 'Assign a user' button
- Add the email (Microsoft Account or AAD Account) of the user 

## Access to Azure Resources

If the user needs access to azure resources (such as Azure App Services, Azure Key Vault or Azure DNS), the user must be created in the AAD tenant and have 'Contributor' or 'Owner' role to the subscription containing the Azure resources.