
# Personal Growth

## Topics to cover

### [Design Patterns](#design-patterns-notes)
 - [ ]  Abstract Factory
 - [ ]  Builder
 - [ ]  Factory Method
 - [ ]  Prototype
 - [X]  Singleton
 - [ ]  Adapter
 - [ ]  Bridge
 - [ ]  Composite
 - [ ]  Decorator
 - [ ]  Facade
 - [ ]  Flyweight
 - [ ]  Proxy
 - [ ]  Chain of Resp.
 - [ ]  Command
 - [ ]  Interpreter
 - [ ]  Iterator
 - [ ]  Mediator
 - [ ]  Memento
 - [ ]  Observer
 - [ ]  State
 - [ ]  Strategy
 - [ ]  Template Method
 - [ ]  Visitor

### [dotnet core](#dotnet-core-notes)
 - [X]  [Introduction](#introduction)
 - [ ]  Getting Started
 - [ ]  HTTP
 - [ ]  Middleware
 - [ ]  Routing
 - [ ]  Controllers and IActionResult
 - [ ]  Model Binding and Validations
 - [ ]  Razor Views
 - [ ]  Layout Views
 - [ ]  Partial Views
 - [ ]  View Components
 - [X]  [Dependency Injection](#dependency-injection)
 - [X]  [Environments](#environments)
 - [ ]  Configurations
 - [ ]  xUnit
 - [ ]  CRUD Operations
 - [ ]  Tag Helpers
 - [ ]  Entity Framework Core
 - [ ]  Unit Testing [Advanced, Moq & Repository Pattern]
 - [ ]  Logging and Serilog
 - [ ]  Filters
 - [ ]  Error Handling
 - [ ]  SOLID Principles
 - [ ]  Clean Architecture
 - [ ]  Identity, Authorization
 - [ ]  Minimal API (Asp.Net Core 7)
 - [ ]  Extra: C# Essentials
 - [ ]  The End

### React JS
### Material UI
### GIT
### Azure Dev Ops
### SOLID Design Principles
### Cloud (Azure)

## Study Notes
### Design Patterns Notes
#### Singleton

> Only one instance should be created in the lifetime.

### dotnet core Notes

#### Introduction
 - Modules:
    - ASP.Net Core MVC
    - ASP.Net Core Web API
    - ASP.Net Core Razor Pages
    - ASP.Net Core Blazor
 - Cross Platform, can be hosted on Win, Linux, Mac
 - Can be hosted on different servers Kestrel, IIS, Nginx, Docker, Apache
 - ASP.Net Core Supports MS Azure Out of the Box
 - ASP.Net Web forms has performance issues because of server events(Page life cycle) and View State
 - ASP.Net MVC has performance issues due to dependencies on ASP.Net(e.g. System.Web.dll)
 - ASP.Net Core has built in support for Dependency Injection while ASP.Net MVC has optional and ASP.Net Webforms no support

`WebApplication.CreateBuilder(args)` builder loads Configuration, Environment and Services

#### Middleware
```csharp
UseWhen(predicate,Action);
```

#### Dependency Injection

```csharp
var builder = WebApplication.CreateBuilder(args);
builder.Services.Add(new ServiceDescriptor(typeof(Abstraction),typeof(ConcreteImplementation),ServiceLifetime);
// or
builder.Services.AddTransient<Abstraction,ConcreteImplementation>();
builder.Services.AddScoped<Abstraction,ConcreteImplementation>();
builder.Services.AddSingleton<Abstraction,ConcreteImplementation>();
```
Constructor Injection is to use DI to resolve abstractions in constructor, and when done in Methods, it is called Method Injection
```csharp
public Task SomeMethod([FromService] SomeInterface someInterface){}
```
**ServiceLifetime**:
 - Transient: Per Injection, if in a request 3 injections are required, 3 objects will be created, disposed when request ends(similar to scoped)
 - Scoped: Browser Request, if in a request 3 injections are required, 1 object will be created and shared, disposed when request ends
 - Singleton: Only one object is created and is shared till lifetime of the service, when application ends

**Child Scope**
Use `ServiceLifetime.Scoped`

Please note: For EntityFramework services, it is internally managed by EntityFramework

```csharp
using(IServiceScope scope = IServiceScopeFactory.CreateScope())
{
    var service = scope.ServiceProvider.GetRequiredService<Abstraction>();
    /// service must implement IDisposable
}
```
**DI in Views**
```csharp
@inject Abstraction abstraction
```

#### Environments

on Development environment variables are set in launchSettings.json under different profiles under environmentVariables->`ASPNETCORE_ENVIRONMENT` or `DOTNET_ENVIRONMENT`

You can set on Powershell> `$Env:ASPNETCORE_ENVIRONMENT="SomeValue"`
You can set on cmd> `SET ASPNETCORE_ENVIRONMENT="SomeValue"`

`dotnet run` runs with launchsettings configuration
`dotnet run --no-launch-profile` runs with envirnoment set to Production and no launch profile

`app.Environment` to use Envirnoment related properties and method

For Dependency Injection you get `IWebHostEnvironment` 

You can also use Tag Helper like <environment></environment> to perform environment specific rendering in ASP.Net, exclude and include are attributes commonly used
```html
<environment include"Development">someContent</environment>
```

Sample code:

> Program.cs

```csharp
/// Builder
var builder = WebApplication.CreateBuilder(args);
// builder.Services
// builder.Configuration
// builder.Environment

/// Application
var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    /// Shows Detailed Exception Details
    app.UseDeveloperExceptionPage();
}

app.Run();
```

> Run on cmd

```batch
dotnet run --no-launch-profile
```
