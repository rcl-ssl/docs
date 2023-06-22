---
title: SDK
description: The RCL SSL SDK provides a C# library to make authorized requests to the RCL Public API 
has_children: false
nav_order: 8
---

# RCL SSL SDK
![Nuget](https://img.shields.io/nuget/v/RCL.SSL.SDK)

The [RCL SSL SDK](https://github.com/rcl-ssl/RCL.SDK) provides a C# .NET Core library to make authorized requests to the [RCL SSL API](../api/api.md). The SDK can be used to renew certificates created in th [RCL SSL Portal](../portal/portal.md). In this section, you will learn how to use the SDK.

## Project's GitHub Page

The project's GitHub page is located at :

[https://github.com/rcl-ssl/RCL.SSL.SDK](https://github.com/rcl-ssl/RCL.SSL.SDK)

## Installing the SDK

You can install the SDK from NuGet :

```
Install-Package RCL.SSL.SDK
```

## Configure the Application using the SDK

Configure the application consuming the SDK by using the app's configuration files (appsettings.json, local.settings.json) or UserSecrets for testing.

### Example Settings in UserSecrets

```
{
  "RCLSDK:ClientId": "4tr56ff4aa-7nn5-4g53-kk2f-6yegdf564435eecf",
  "RCLSDK:ClientSecret": "cheyvd456eh~_7-f7lNI34B01.xIDUMHh",
  "RCLSDK:TenantId": "23fdvrxffc-bc3c-4323-b4c2-4502c3b9b0e6",
  "RCLSDK:SubscriptionId": "879",
  "RCLSDK:ApiBaseUrl": "https://rclapi.azure-api.net/public",
  "RCLSDK:SourceApplication": "RCL SSL SDK"
}
```

The configuration must be changed to match the **User's AAD Application** credentials as explained below.

## Register an AAD Application

To obtain the values for the AAD configuration, a user would would need to Register an AAD Application and obtain the credentials for the application.

Please refer to the following link for instructions :

- [Register an AAD Application](../authorization/aad-application)

## Get the AAD Credentials

To obtain the following credentials from the AAD application:

- ClientId
- ClientSecret
- TenantId

follow the instructions in this link :

- [Get the AAD Application Credentials](../authorization/aad-application#get-the-aad-application-credentials)

## Get the SubscriptionId

Get the **Subscription Id** in the RCL SSL Portal.

![install](../images/autorenew_configure/add_subscriptionid.png)

- Scroll down and copy the 'Subscription Id' 

![install](../images/autorenew_configure/add_subscriptionid2.png)

## Set Access Control for the AAD Application

Access Control must be set for the AAD application to access a user's Azure Resources.

Please refer to the following link for instructions :

- [Set Access Control for the AAD application](../authorization/access-control-app)

## Register the AAD Application's ``Client Id`` in the RCL SSL Portal

The AAD Application must be associated with a user's RCL SSL subscription. This is achieved by registering the AAD Application's ``Client Id`` in the **RCL SSL Portal**.

To add the AAD Application's ``Client Id`` to the portal, please follow the instructions in this link :

- [Add the Client Id in the RCL SSL Portal](../api/authorization#add-the-client-id-in-the-rcl-lets-encrypt-portal)

## Add the Services

 Set up the application using the SDK to use **Dependency Injection (DI)**; and add the SDK services ``AddRCLSDKService`` to the ``IServiceCollection``.

### Example Dependency Injection

```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;

namespace RCL.SDK.Test
{
    public static class DependencyResolver
    {
        public static ServiceProvider ServiceProvider()
        {
            ConfigurationBuilder builder = new ConfigurationBuilder();
            builder.AddUserSecrets<TestProject>();
            IConfiguration configuration = builder.Build();

            IServiceCollection services = new ServiceCollection();

            services.AddRCLSDKService(options => configuration.Bind("RCLSDK", options));

            return services.BuildServiceProvider();
        }
    }

    public class TestProject
    {
    }
}
```

### Example ASP.NET Core App

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddRCLSDKService(options => Configuration.Bind("RCLSDK", options));
}
```

## Inject the ``CertificateService`` in your Class or Controller

### Example 

```csharp
namespace RCL.SDK.Test
{
    public class CertificateServiceTest
    {
        private readonly ICertificateRequestService _certificateRequestService;

        public CertificateServiceTest()
        {
            _certificateRequestService = (ICertificateRequestService)DependencyResolver
                 .ServiceProvider().GetService(typeof(ICertificateRequestService));
        }
    }
}
```

### Example ASP.NET Core

```csharp
namespace RCL.SDK
{
    public class GetCertificate
    {
        private readonly ICertificateRequestService _certificateRequestService;

        public GetCertificate( ICertificateRequestService certificateRequestService)
        {
            _certificateRequestService = certificateRequestService;
        }
    }
}
```

## Using the ``CertificateService``

### Run the Certificate Test API to test the API connectivity

[POST Certificate Test](../api/post-certificate-test.md)

```csharp
await _certificateRequestService.GetTestAsync();
```

### Get a Certificate in a User's Subscription

[POST Certificate](../api/post-certificate.md)

```csharp
Certificate certificate = new Certificate
{
    certificateName = "shopeneur.com"
};

Certificate _certificate = await _certificateRequestService.GetCertificateAsync(certificate);
```

### Get a List of Certificates that should be renewed in a User's Subscription

[POST Certificate Renew Get List](../api/post-certificate-renew-get-list.md)

```csharp
List<Certificate> certificates = await _certificateRequestService.GetCertificatesToRenewAsync();
```

### Renew a Certificate in a User's Subscription

[POST Certificate Renew](../api/post-certificate.renew.md)

```csharp
Certificate certificate = new Certificate
{
    certificateName = "shopeneur.com"
};

await _certificateRequestService.RenewCertificateAsync(certificate);
```

## Production Apps

The following productions apps were built with the RCL SSL SDK :

- [RCL SSL AutoRenew Function](../autorenew/autorenew.md)
