---
title: AAD User Account
description: Learn how to create an Active Directory Organization User Account for use in RCL applications
parent: Authorization
nav_order: 2
---

# Azure Active Directory Organization Account
**V6.0.10**

An Azure Active Directory (AAD) organization account is required to sign in to the [RCL Portal](../portal/portal.md) to manage Azure resources (App Services, DNS, Key Vault, etc.). An organization account is also called a **‘Work or School’ account**. Follow these steps to use an AAD account in the RCL Portal.

- In the Azure Portal, search for the **Azure Active Directory** and open it

![image](../images/authorization_signin/subscribe-aad-open.png)

- In your tenant, click the ‘Users’ link

![image](../images/authorization_signin/subscribe-aad-user-new.png)

# Use an Exiting User Account

You can select an exiting user account who is a **member** of the tenant to login to RCL. **Guest users cannot be used.**

![image](../images/authorization_signin/subscribe-aad-user-member.png)

# Create a New User Account

You can also create a new user account to sign in to the RCL Portal.

- Click the ‘New user’ link to create a new user

![image](../images/authorization_signin/subscribe-aad-user-new.png)

- Add the new user

![image](../images/authorization_signin/subscribe-aad-user-add.png)

- Ensure the new user is a **member** in your organization

![image](../images/authorization_signin/subscribe-aad-user-member.png)

- You can use this new AAD organization account to login in to any of the RCL applications.

# Sign In

You should now sign in to the Azure Portal using the existing or new AAD Work or School account.

It is strongly recommended that you sign in with this AAD Work or School account in the Azure Portal when you subscribe to the RCL Portal App in the Azure Marketplace.

# Access Control

To access resources in you Microsoft Azure account a further step is required. Your AAD Work or School account must be an 'Administrator' or 'Owner' on the subscription containing your azure resources. 

Refer to the following link for more information :

- [Set Access Control for the AAD user](./access-control-user)



