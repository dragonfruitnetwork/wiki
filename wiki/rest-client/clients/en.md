# REST Clients
An `ApiClient` is used to perform HTTP requests and is designed to be highly customisable. They are designed to only require a single instance for the lifetime of the program, and as such should be `static` or Singleton (if using dependency injection).

To create a basic client, a default serializer type will be required. This will be used when a type does not have a dedicated serializer type assigned to it. By default, two serialzers are provided out-the-box:

- `ApiJsonSerializer`
- `ApiXmlSerializer`

```cs
using DragonFruit.Data;
using DragonFruit.Data.Serializers;

namespace DataApp;

public static class Program
{
    // use ApiJsonSerializer as the default serializer
    internal static ApiClient Client = new ApiClient<ApiJsonSerializer>();
}
```

Additionally, the `Client.UserAgent` can be set if a User-Agent header is desired and a custom `HttpMessageHandler` factory can be defined via `Client.Handler` (although the default should be sufficient for 99% of all use cases)

## Overriding Functions
Creating custom `ApiClient` types is possible and can be helpful when overriding specific functionality regarding building requests, constructing clients and handlers.

`ApiClient` exposes a number of overridable methods that can be used to tailor the client functionality specific to your needs:

- `CreateHandler()` - method used to create a `HttpMessageHandler` provided to the internal `HttpClient`
    > This method is designed to be used to forcibly wrap the user defined handler (`ApiClient.Handler` property) to allow low-level modifications to requests before they're made. If this is overidden, the class should be sealed to prevent bypassing any wrappers.
- `CreateClient()` - method used to create the internal `HttpClient`
- `BuildRequest(ApiRequest request, string expectedContentType)` - method used to convert an `ApiRequest` class to a `HttpRequestMessage` instance
- `ValidateAndProcess<T>(HttpResponseMessage response, ApiSerializer serializer, CancellationToken cancellationToken) where T : class` - takes the response message, validates the response code and deserializes the response

For example, when using the library on a WebAssembly project, the default `HttpMessageHandler` cannot be used. As a result, the following override can be used to restore functionality:

```cs
using System.Net.Http;
using DragonFruit.Data;

namespace DataExample;

public class WasmClient : ApiClient
{
    protected override HttpClient CreateClient() => new HttpClient();
}
```
