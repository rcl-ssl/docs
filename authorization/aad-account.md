---
title: AAD User Account
description: Learn how to create an Active Directory Organization User Account for use in RCL applications
parent: Authorization
nav_order: 2
---

# Microsoft Entra ID Account
**V8.0**

An Microsoft Entra ID (formerly AAD) organization account is required to sign in to the [RCL SSL Portal](../portal/portal.md) to manage Azure Resources (App Services, DNS, Key Vault, etc.). An organization account is also called a **‘Work or School’ account**. Follow these steps to use an organizaion account in the RCL SSL Portal.

- In the Azure Portal, open **Microsoft Entra ID** 

- In your tenant, click the ‘Users’ link

![image](../images/authorization_signin/subscribe-aad-user-new.png)

# Use an Exiting User Account

You can select an exiting user account who is a **member** of the tenant to login to the RCL SSL Portal. **Guest users cannot be used.**

![image](../images/authorization_signin/subscribe-aad-user-member.png)

# Create a New User Account

You can also create a new user account to sign in to the RCL SSL Portal.

- Click the ‘New user’ link to create a new user

![image](../images/authorization_signin/subscribe-aad-user-new.png)

- Add the new user

![image](../images/authorization_signin/subscribe-aad-user-add.png)

- Ensure the new user is a **member** in your organization

![image](../images/authorization_signin/subscribe-aad-user-member.png)

- You will need to associate this new organization account to login in to the RCL SSL Portal.

# Access Control

To access resources in you Microsoft Azure account a further step is required. Your AAD Work or School account must be an 'Administrator' or 'Owner' in the Subscription containing your azure resources. 

Refer to the following link for more information :

- [Set Access Control for the organization user](./access-control-user)



