---
title: Access Control - AAD App
parent: Authorization
nav_order: 5
---

## Set Access Control for the AAD application

A user will need to provide **Access Control** to the [AAD Application](./aad-application) for it to manage the user's Azure Services (App Services, DNS Zone and Key Vault).


- Go to Azure subscriptions, and open the subscription

- In the subscription, click on 'Access control (IAM)' and add a new **role assignment**

![install](../images/authorization_access_control/add_role.PNG)

- Select the 'Contributor' role

- Search for the AAD App that was registered and select it. (If you did not register an AAD app previously, please follow the instruction in this link : [Registering an AAD Application](../authorization/aad-application))


![install](../images/authorization_access_control/add_role2.PNG)

- Click the 'Save' button 

- In the 'Role assignments' tab, you will see the new role assignment you just added

![install](../images/authorization_access_control/add_role3.PNG)

## Access Policies for Key Vault

If a user is creating SSL/TLS certificates for **Azure Key Vault**, they will need to set **Access policies** for the certificate in Key Vault

- In Key Vault, click on 'Access policies' and 'Add Access Policy'

![install](../images/authorization_access_control/key_vault.PNG)

- In the 'Certificate permissions' dropdown, select all **16 permissions**, including 'Purge' permission.

![install](../images/authorization_access_control/key_vault2.PNG)

- Then , click on 'Select principal'

- Search for the application that was registered and select it 

![install](../images/authorization_access_control/key_vault3.PNG)

- Click the 'Add' button when you are done

![install](../images/authorization_access_control/key_vault4.PNG)

- Click the 'Save' button to save the access policy

![install](../images/authorization_access_control/key_vault5.PNG)

- The newly added access policy will be displayed

![install](../images/authorization_access_control/key_vault6.PNG)

