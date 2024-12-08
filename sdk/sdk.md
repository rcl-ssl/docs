---
title: SDK
description: Using the RCL SSL API to get and renew certificates created in the RCL SSL portal
has_children: true
nav_order: 11
---

# RCL SSL SDK
**V8.0**

The RCL SSL SDK provides a C# .NET Core library to make authorized requests to the [RCL SSL API](../api/api.md). Use the SDK to get, create and renew SSL/TLS certificates in a user's subscription in the [RCL Portal](../portal/portal.md).

## Prerequisites

Before you can use the SDK, you must first :

- Obtain an [API Key](./authorization.md)
- Create the [CSR Information](../portal/csr-info.md)

## Install the SDK

You will install the SDK as a Nuget package. 

![image](../images/sdk/nuget.PNG)

## Adding the SDK to an Application

Add the SDK to your application in the ```Program.cs``` file using Dependency Injection

```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using RCL.SSL.SDK;

IServiceCollection services = new ServiceCollection();

ConfigurationBuilder builder = new ConfigurationBuilder();
builder.AddUserSecrets<TestProject>();
IConfiguration configuration = builder.Build();

services.AddRCLSSLAPIService(options => configuration.Bind("RCLSSLAPI", options));

ServiceProvider serviceProvider = services.BuildServiceProvider();

class TestProject { }
```

## Configuration

Configure the SDK in ```User Secrets```


### Authorization

Obtain the [API Key](./authorization.md) in the **Subscription > API Key** page in the RCL SSL Portal.

You will use the API Key to configure the SDK.

## Subscription

To use the SDK, you must use your subscription. You can obtain the subscription value from the **Subscription > Details** page in the RCL SSL Portal.

![image](../images/api_authorization/subscription.png)

Use the API Key and Subscription to configure the SDK :

```json
{
  "RCLSSLAPI:ApiBaseUrl": "https://rclapi.azure-api.net/prod/v3",
  "RCLSSLAPI:ApiKey": "546yt546-yt67-038usd-8876g",
  "RCLSSLAPI:Subscription": "sud56298tr",
  "RCLSSLAPI:Source": "Test"
}
```

## Create a Certificate Order for a Stand Alone Certificate

You will first need to create a certificate order before you can create a Stand Alone certificate.

```csharp
#nullable disable

using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using RCL.SSL.SDK;

IServiceCollection services = new ServiceCollection();

ConfigurationBuilder builder = new ConfigurationBuilder();
builder.AddUserSecrets<TestProject>();
IConfiguration configuration = builder.Build();

services.AddRCLSSLAPIService(options => configuration.Bind("RCLSSLAPI", options));

ServiceProvider serviceProvider = services.BuildServiceProvider();

// Create an Order for a Stand ALone Certificate
async Task<Certificate> CreateStandAloneOrderAsync()
{
    ICertificateService certificateService = (ICertificateService)serviceProvider.GetService(typeof(ICertificateService));
    
    Certificate certificate = new Certificate
    {
        certificateName = "shopeneur.com",
        rootDomain = "shopeneur.com",
        challengeType = RCLSSLAPIConstants.dnsChallenge,
        email = "rcl@mail.com",
        password = "password123",
        target = RCLSSLAPIConstants.targetStandAlone,
        isSAN = false
    };

    Certificate certificateOrder = await certificateService.CertificateCreateOrderAsync(certificate);

    return certificateOrder;
}

Certificate certificate =  await CreateStandAloneOrderAsync();

class TestProject { }
```






