---
title: SDK
has_children: false
nav_order: 7
---

# RCL SDK

The [RCL SDK](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.SDK) provides a simple C# .NET Core 3.1 library to make authorized requests to the [RCL API](../api/api) . In this section, you will learn how to use the SDK.

## Project's GitHub Page

The project's GitHub page is located at :

[https://github.com/rcl-ssl/RCL.SDK](https://github.com/rcl-ssl/RCL.SDK)

## Installing the SDK

You can install the SDK from NuGet :

```
Install-Package RCL.SDK
```

## Configure the Application Consuming the SDK

Configure the application consuming the SDK (Console App, ASP.NET Core App, Function App, etc.) by using the app's configuration files (appsettings.json, local.settings.json, Azure Configuration) or UserSecrets for testing.

### Example Settings in UserSecrets

```
  "Auth:client_id": "g54663-hdggfgt-54ggvfy-6478hsfd",
  "Auth:client_secret": "~gdttrffd-645gbdgfT-uyrTT4_",
  "Auth:tenantId": "5547785-76535554-8476534",

  "RCLSDK:apiEndPoint": "https://rclapi.azure-api.net",
  "RCLSDK:armResource": "https://management.core.windows.net",
  "RCLSDK:keyVaultResource": "https://vault.azure.net"
```

The ``auth`` configuration must be changed to match the user's AAD Application credentials.

The other configurations will remain the same.

### Register an AAD Application

To obtain the values for the ``Auth`` configuration, a user would would need to Register an AAD Application and obtain the credentials for the application.

Please refer to the following link for instructions :

- [Register an AAD Application](../authorization/aad-application)

### Set Access Control for the AAD Application

Access Control must be set for the AAD application to access a user's Azure Resources.

Please refer to the following link for instructions :

- [Set Access Control for the AAD application](../authorization/access-control-app)

### Register the AAD Application's ``Client Id`` in the RCL Portal

The AAD Application must be associated with a user's RCL subscription. This is achieved by registering the AAD Application's ``Client Id`` in the **RCL Portal**.

To add the AAD Application's ``Client Id`` to the portal, please follow the instructions in this link :

- [Add the Client Id in the RCL Portal](../api/authorization#add-the-client-id-in-the-rcl-lets-encrypt-portal)

## Add the Services

 Set up the application consuming the SDK to use **Dependency Injection (DI)**; and add the SDK services ``AddAuthTokenService``, ``AddRCLSDK`` to the ``IServiceCollection``.

### Example Console App

```csharp
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;

namespace RCL.SDK.ConsoleSample
{
    public static class Startup
    {
        public static ServiceProvider ServiceProvider()
        {
            ConfigurationBuilder builder = new ConfigurationBuilder();
            builder.AddUserSecrets<ConsoleProject>();
            IConfiguration Configuration = builder.Build();

            IServiceCollection services = new ServiceCollection();

            // Add the SDK Services
            services.AddAuthTokenService(options => Configuration.Bind("Auth", options));
            services.AddRCLSDK(options => Configuration.Bind("RCLSDK", options));

            return services.BuildServiceProvider();
        }
    }

    public class ConsoleProject
    {
    }
}
```

### Example ASP.NET Core App

```csharp
// This method gets called by the runtime. Use this method to add services to the container.
public void ConfigureServices(IServiceCollection services)
{
    // Add the SDK Services
    services.AddAuthTokenService(options => Configuration.Bind("Auth", options));
    services.AddRCLSDK(options => Configuration.Bind("RCLSDK", options));

    services.AddRazorPages();
}
```

### Example Function App

```csharp
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;

[assembly: FunctionsStartup(typeof(RCL.SDK.FunctionSample.Startup))]
namespace RCL.SDK.FunctionSample
{
    public class Startup : FunctionsStartup
    {
        public override void Configure(IFunctionsHostBuilder builder)
        {
            IServiceCollection services = builder.Services;

            IConfiguration configuration = builder.GetContext().Configuration;

            // Add the SDK Services
            services.AddAuthTokenService(options => configuration.Bind("Auth", options));
            services.AddRCLSDK(options => configuration.Bind("RCLSDK", options));
        }
    }
}
```

## Inject the ``CertificateService`` in your Class or Controller

### Example Console App

```csharp
using System;
using System.Threading.Tasks;

namespace RCL.SDK.ConsoleSample
{
    class Program
    {
        private static readonly ICertificateService _certificateService;

        static Program()
        {
            _certificateService = (ICertificateService)Startup
                .ServiceProvider().GetService(typeof(ICertificateService));
        }

        static async Task Main(string[] args)
        {
        }
    }
}
```

### Example ASP.NET Core App

```csharp
namespace RCL.SDK.AspnetSample.Pages
{
    public class IndexModel : PageModel
    {
        private readonly ICertificateService _certificateService;

        public IndexModel(ICertificateService certificateService)
        {
            _certificateService = certificateService;
        }
}
```

### Example Function App

```csharp
namespace RCL.SDK.FunctionSample
{
    public class GetCertificate
    {
        private readonly ICertificateService _certificateService;

        public GetCertificate(ICertificateService certificateService)
        {
            _certificateService = certificateService;
        }
    }
}
```

## Using the ``CertificateService``

### Get a Certificate by its name

Make a GET request to the [Certificate API](../api/get-certificate)

```csharp
CertificateResponse certificateResponse = await _certificateService
.GetCertificateAsync("contoso.com");
```

### Get a List of Certificates in a User Subscription

Make a GET request to the [CertificateList API](../api/get-certificate-list)

```csharp
List<CertificateResponse> lstCertificateResponse = await _certificateService
.GetCertificatesListAsync();
```

### Make a Post request to Renew Certificates

Make a POST request to the [CertificateRenewal API](../api/post-certificate-renewal)

```csharp
// There are no Azure Key Vault certificates in the user subscription 
List<CertificateResponse> lstCertificateResponse = await _certificateService
.PostCertificateRenewalAsync(false);

// There are Azure Key Vault certificates in the user subscription 
List<CertificateResponse> lstCertificateResponse = await _certificateService
.PostCertificateRenewalAsync(true);
```

### Update a Certificate's ``remoteCreateDate`` when it is Saved in a Server

Make a POST request to the [Certificate API](../api/post-certificate)

```csharp
 CertificateResponse data = new CertificateResponse
  {
    id = 158,
    name = "contoso.com",
    remoteCreateDate = DateTime.Now,
    remoteCreate = "prod-server"
  };

CertificateResponse certificateResponse = await _certificateService
.PostCertificateAsync(data);
```

## Sample Projects

The following sample projects are available for review on the [SDK's GitHub Project Page](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.SDK)

- [Sample Console App](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.SDK/tree/master/samples/RCL.LetsEncrypt.SDK.ConsoleSample)
- [Sample ASP.NET Core App](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.SDK/tree/master/samples/RCL.LetsEncrypt.SDK.AspnetSample)
- [Sample Function App](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.SDK/tree/master/samples/RCL.LetsEncrypt.SDK.FunctionSample)

## Production Apps

The following productions apps were built with the RCL SDK :

- [RCL AutoRenew](https://github.com/rcl-letsencrypt-auto-ssl/RCL.LetsEncrypt.AutoRenew) Function app
