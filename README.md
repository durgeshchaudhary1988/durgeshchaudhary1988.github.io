# Personal Growth

## Topics to cover

### Design Patterns
 - [ ] Abstract Factory
 - [ ] Builder
 - [ ] Factory Method
 - [ ] Prototype
 - [X] Singleton
 - [ ] Adapter
 - [ ] Bridge
 - [ ] Composite
 - [ ] Decorator
 - [ ] Facade
 - [ ] Flyweight
 - [ ] Proxy
 - [ ] Chain of Resp.
 - [ ] Command
 - [ ] Interpreter
 - [ ] Iterator
 - [ ] Mediator
 - [ ] Memento
 - [ ] Observer
 - [ ] State
 - [ ] Strategy
 - [ ] Template Method
 - [ ] Visitor

### dotnet core
 - [ ] Introduction
 - [ ] Getting Started
 - [ ] HTTP
 - [ ] Middleware
 - [ ] Routing
 - [ ] Controllers and IActionResult
 - [ ] Model Binding and Validations
 - [ ] Razor Views
 - [ ] Layout Views
 - [ ] Partial Views
 - [ ] View Components
 - [ ] Dependency Injection
 - [ ] Environments
 - [ ] Configurations
 - [ ] xUnit
 - [ ] CRUD Operations
 - [ ] Tag Helpers
 - [ ] Entity Framework Core
 - [ ] Unit Testing [Advanced, Moq & Repository Pattern]
 - [ ] Logging and Serilog
 - [ ] Filters
 - [ ] Error Handling
 - [ ] SOLID Principles
 - [ ] Clean Architecture
 - [ ] Identity, Authorization
 - [ ] Minimal API (Asp.Net Core 7)
 - [ ] Extra: C# Essentials
 - [ ] The End

### React JS
### Material UI
### GIT
### Azure Dev Ops
### SOLID Design Principles
### Cloud (Azure)

## Study Notes
### Design Patterns
#### Singleton
Only one instance should be created in the lifetime.

### dotnet core
#### Middleware
```
UseWhen(predicate,Action);
```

#### Dependency Injection

```
var builder = WebApplication.CreateBuilder(args);
builder.Services.Add(new ServiceDescriptor(typeof(Abstraction),typeof(ConcreteImplementation),ServiceLifetime);
```
Constructor Injection is to use DI to resolve abstractions in constructor, and when done in Methods, it is called Method Injection
```
public Task SomeMethod([FromService] SomeInterface someInterface){}
```
**ServiceLifetime**:
 - Transient: Per Injection, if in a request 3 injections are required, 3 objects will be created, disposed when request ends(similar to scoped)
 - Scoped: Browser Request, if in a request 3 injections are required, 1 object will be created and shared, disposed when request ends
 - Singleton: Only one object is created and is shared till lifetime of the service, when application ends
