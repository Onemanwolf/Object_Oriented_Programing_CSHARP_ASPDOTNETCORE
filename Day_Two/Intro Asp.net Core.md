# Introduction to ASP.NET Core


ASP.NET Core is a cross-platform, high-performance, open-source framework for building modern, cloud-enabled, Internet-connected apps. With ASP.NET Core, you can:

- Build web apps and services, Internet of Things (IoT) apps, and mobile backends.
- Use your favorite development tools on Windows, macOS, and Linux.
- Deploy to the cloud or on-premises.
- Run on .NET Core.

# Why choose ASP.NET Core?

Millions of developers use or have used [ASP.NET 4.x](https://docs.microsoft.com/en-us/aspnet/overview) to create web apps. ASP.NET Core is a redesign of ASP.NET 4.x, including architectural changes that result in a leaner, more modular framework.

ASP.NET Core provides the following benefits:

- A unified story for building web UI and web APIs.
- Architected for testability.
- [Razor Pages](https://docs.microsoft.com/en-us/aspnet/core/razor-pages/?view=aspnetcore-3.1) makes coding page-focused scenarios easier and more productive.
[Blazor](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.1) lets you use C# in the browser alongside JavaScript. Share server-side and client-side app logic all written with .NET.
- Ability to develop and run on Windows, macOS, and Linux.
- Open-source and [community-focused](https://live.asp.net/).
- Integration of modern, client-side frameworks and development workflows.
- Support for hosting Remote Procedure Call (RPC) services using gRPC.
- A cloud-ready, environment-based configuration system.
- Built-in [dependency injection](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-3.1).
A lightweight, [high-performance](https://github.com/aspnet/benchmarks), and modular HTTP request pipeline.
- Ability to host on the following:
     - Kestrel
     - IIS
     - HTTP.sys
     - Nginx
     - Apache
     - Docker

- [Side-by-side versioning](https://docs.microsoft.com/en-us/dotnet/standard/choosing-core-framework-server#side-by-side-net-versions-per-application-level).
- Tooling that simplifies modern web development.

# Build web APIs and web UI using ASP.NET Core MVC
ASP.NET Core MVC provides features to build web APIs and web apps:

- The [Model-View-Controller (MVC)](https://docs.microsoft.com/en-us/aspnet/core/mvc/overview?view=aspnetcore-3.1) pattern helps make your web APIs and web apps testable.
- [Razor Pages](https://docs.microsoft.com/en-us/aspnet/core/razor-pages/?view=aspnetcore-3.1) is a page-based programming model that makes building web UI easier and more productive.
- [Razor markup](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-3.1) provides a productive syntax for Razor Pages and MVC views.
- [Tag Helpers](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-3.1) enable server-side code to participate in creating and rendering HTML elements in Razor files.
- Built-in support for [multiple data formats and content negotiation](https://docs.microsoft.com/en-us/aspnet/core/web-api/advanced/formatting?view=aspnetcore-3.1) lets your web APIs reach a broad range of clients, including browsers and mobile devices.
- [Model binding](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-3.1) automatically maps data from HTTP requests to action method parameters.
- [Model validation](https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-3.1) automatically performs client-side and server-side validation.

# Client-side development

ASP.NET Core integrates seamlessly with popular client-side frameworks and libraries, including [Blazor](https://docs.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-3.1), [Angular](https://docs.microsoft.com/en-us/aspnet/core/client-side/spa/angular?view=aspnetcore-3.1), [React](https://docs.microsoft.com/en-us/aspnet/core/client-side/spa/react?view=aspnetcore-3.1), and [Bootstrap](https://getbootstrap.com/). For more information, see Introduction to ASP.NET Core Blazor and related topics under Client-side development.


# ASP.NET Core target frameworks
ASP.NET Core 3.x and later can only target .NET Core. Generally, ASP.NET Core is composed of [.NET Standard](https://docs.microsoft.com/en-us/dotnet/standard/net-standard) libraries. Libraries written with [.NET Standard 2.0 run on any .NET platform that implements .NET Standard 2.0](https://docs.microsoft.com/en-us/dotnet/standard/net-standard#net-implementation-support).

There are several advantages to targeting .NET Core, and these advantages increase with each release. Some advantages of .NET Core over .NET Framework include:

- Cross-platform. Runs on Windows, macOS, and Linux.
- Improved performance
- [Side-by-side versioning](https://docs.microsoft.com/en-us/dotnet/standard/choosing-core-framework-server#side-by-side-net-versions-per-application-level)
- New APIs
- Open source

# Recommended learning path
We recommend the following sequence of tutorials for an introduction to developing ASP.NET Core apps:

Follow a tutorial for the app type you want to develop or maintain.


| App type | Scenario | Tutorial |
|--------|-------|------|
Web app | New server-side  web UI development |	[Get started with Razor Pages](https://docs.microsoft.com/en-us/aspnet/core/tutorials/razor-pages/razor-pages-start?view=aspnetcore-3.1) |
|Web app |	Maintaining an MVC app | [Get started with MVC](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-3.1) |
|Web app | Client-side web UI development |	[Get started with Blazor](https://dotnet.microsoft.com/learn/aspnet/blazor-tutorial/intro) |
| Web API |	RESTful HTTP services |	[Create a web API†](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-3.1) |
| Remote Procedure Call app | Contract-first services using Protocol Buffers | [Get started with a gRPC service](https://docs.microsoft.com/en-us/aspnet/core/tutorials/grpc/grpc-start?view=aspnetcore-3.1) |
Real-time app |	Bidirectional communication between servers and connected clients	| [Get started with SignalR](https://docs.microsoft.com/en-us/aspnet/core/tutorials/signalr?view=aspnetcore-3.1) |

Follow a tutorial that shows how to do basic data access.


|Scenario	| Tutorial |
|----------|-----------|
|New development |[	Razor Pages with Entity Framework Core](https://docs.microsoft.com/en-us/aspnet/core/data/ef-rp/intro?view=aspnetcore-3.1) |
|Maintaining an MVC app	|[MVC with Entity Framework Core](https://docs.microsoft.com/en-us/aspnet/core/data/ef-mvc/intro?view=aspnetcore-3.1) |
3. Read an overview of ASP.NET Core fundamentals that apply to all app types.

4. Browse the table of contents for other topics of interest.

†There's also an [interactive web API tutorial](https://docs.microsoft.com/en-us/learn/modules/build-web-api-net-core). No local installation of development tools is required. The code runs in an [Azure Cloud Shell](https://azure.microsoft.com/features/cloud-shell/) in your browser, and [curl](https://curl.haxx.se/) is used for testing.

# Migrate from .NET Framework

For a reference guide to migrating ASP.NET 4.x apps to ASP.NET Core, see [Migrate from ASP.NET to ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/migration/proper-to-2x/?view=aspnetcore-3.1).

## How to download a sample

Many of the articles and tutorials include links to sample code.

1. [Download the ASP.NET repository zip file](https://codeload.github.com/dotnet/AspNetCore.Docs/zip/master).
2. Unzip the Docs-master.zip file.
3. Use the URL in the sample link to help you navigate to the sample directory.

Preprocessor directives in sample code
To demonstrate multiple scenarios, sample apps use the #define and `#if-#else/#elif-#endif ` preprocessor directives to selectively compile and run different sections of sample code. For those samples that make use of this approach, set the `#define` directive at the top of the `C#` files to define the symbol associated with the scenario that you want to run. Some samples require defining the symbol at the top of multiple files in order to run a scenario.

For example, the following #define symbol list indicates that four scenarios are available (one scenario per symbol). The current sample configuration runs the TemplateCode scenario:

```C#
#define TemplateCode // or LogFromMain or ExpandDefault or FilterInCode
```

To change the sample to run the `ExpandDefault` scenario, define the `ExpandDefault` symbol and leave the remaining symbols commented-out:

```C#
#define ExpandDefault // TemplateCode or LogFromMain or FilterInCode
```

For more information on using [C# preprocessor directives](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/preprocessor-directives/) to selectively compile sections of code, see #define (C# Reference) and #if (C# Reference).

Regions in sample code
Some sample apps contain sections of code surrounded by #region and #endregion C# directives. The documentation build system injects these regions into the rendered documentation topics.

Region names usually contain the word "snippet." The following example shows a region named snippet_WebHostDefaults:

```C#
#region snippet_WebHostDefaults
Host.CreateDefaultBuilder(args)
    .ConfigureWebHostDefaults(webBuilder =>
    {
        webBuilder.UseStartup<Startup>();
    });

#endregion
```

The preceding C# code snippet is referenced in the topic's markdown file with the following line:

```Markdown
[!code-csharp[](sample/SampleApp/Program.cs?name=snippet_WebHostDefaults)]

```

You may safely ignore (or remove) the `#region` and `#endregion` directives that surround the code. Don't alter the code within these directives if you plan to run the sample scenarios described in the topic. Feel free to alter the code when experimenting with other scenarios.

For more information, see Contribute to the [ASP.NET documentation: Code snippets](https://github.com/dotnet/AspNetCore.Docs/blob/master/CONTRIBUTING.md#code-snippets).