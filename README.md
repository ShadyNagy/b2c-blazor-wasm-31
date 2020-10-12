# Azure B2C Blazor WASM Working with 3.1

### Secure an ASP.NET Core Blazor WebAssembly hosted app with Azure Active Directory B2C
### Azure B2C not working in Blazor WASM (netstandard2.1) without the implicit grant so that is the solution

1- Create the app [Microsoft Documentation](https://docs.microsoft.com/en-us/aspnet/core/blazor/security/webassembly/hosted-with-azure-active-directory-b2c?view=aspnetcore-3.1)

2- Copy file AuthenticationService.js from src folder to your Blazor WASM project (B2CWasm.Client) in wwwroot folder.

3- Change index.html in wwwroot folder from
```html
<script src="_content/Microsoft.Authentication.WebAssembly.Msal/AuthenticationService.js"></script>
```
to
```html
<script src="AuthenticationService.js"></script>
```

4- add this package to server
```xml
    <PackageReference Include="Microsoft.Identity.Web" Version="1.1.0" />
```
5- in WeatherForecastController 
```csharp
...
using Microsoft.Identity.Web.Resource;
 ...

public class WeatherForecastController : ControllerBase
{
  ...
  static readonly string[] scopeRequiredByApi = new string[] { "your scop name" };
  ...
  [HttpGet]
  public IEnumerable<WeatherForecast> Get()
  {
    HttpContext.VerifyUserHasAnyAcceptedScope(scopeRequiredByApi);

    ...
  }
```
