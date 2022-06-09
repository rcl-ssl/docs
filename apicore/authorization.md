---
title: API Authorization
description: Obtaining an authorization token for the RCL Core API
parent: RCL Core API
nav_order: 2
---

# Obtaining an Access Token
**V6.0.10**

Steps in acquiring an access token :

- Step 1: Register an AAD Application in the Azure portal
- Step 2: Register the AAD Application's Client Id in the **RCL Portal**
- Step 3: Make a POST request to the AAD Application-specific token endpoint to obtain a token

## Registering an AAD Application

To register an AAD application, please follow the instruction in this link :

- [Registering an AAD Application](../authorization/aad-application)

## Get the AAD Credentials

To obtain the following credentials from the AAD application:

- Client Id
- Client Secret
- Tenant Id

follow the instructions in this link :

- [Get the AAD Application Credentials](../authorization/aad-application#get-the-aad-application-credentials)

## Add the Client Id in the RCL Portal

A user must add the **Client Id** in the **RCL Portal** in order to associate the AAD application with the user's RCL subscription.

- Open the **RCL Portal**

- In the 'Subscription' section, click on 'API Client', then click the 'Register a Client Id' button

![install](../images/api_authorization/client_id.PNG)

- Add the **Client Id** for the AAD application. (To obtain the Client Id from the AAD application, please refer to : [Get the AAD Application Credentials](../authorization/aad-application#get-the-aad-application-credentials)

![install](../images/api_authorization/client_id2.PNG)

- Click the 'Submit' button when you are done.

## Request an Access Token

 To request an access token, use an HTTP POST to the Application-specific Azure AD token endpoint.

 ```
 https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token
 ```

 Replace the `tenantId` placeholder with the **Tenant Id** for the [AAD Application](#get-the-aad-credentials).

 Include the following parameters in the **body** of the POST request in the [Form-UrlEncoded](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) format :

- grant_type : should be : ``client_credentials``
- client_id : the Client Id of the [AAD Application](#get-the-aad-credentials)
- client_secret : the Client Secret of the [AAD Application](#get-the-aad-credentials)
- resource : the RCL Core API resource, should be : ``a9e1b21d-061d-42d6-99d9-115a328cd062/.default``  

### Example Request

 ```
POST /88cd9a7c-bc7c-3426-b9c2-2702c3b6b0e7/oauth2/v2.0/token HTTP/1.1           
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865
&scope=a9e1b21d-061d-42d6-99d9-115a328cd062%2F.default%0A
&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s
&grant_type=client_credentials

 ```

## Service Response

A success response contains a JSON response with an [AuthToken](./models.md#authtoken) in the body of the response. The Access Token can be acquired from the ``AuthToken``.

## Example Response

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

## Use the Access Tokens to Make a Request

To make a request to the RCL Core API, include the access token as a `Bearer` **Authorization** in the header of the request

## Example

```
GET /production/ssl/core/v1/certificate/subscription/I-TKGDBEFH2BEN/get/all
Host: https://rclapi.azure-api.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP...
```