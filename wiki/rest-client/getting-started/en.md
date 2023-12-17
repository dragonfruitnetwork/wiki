# Getting Started
In this guide, we will be creating a basic command-line program that can make a simple GET request to a remote server, and deserialize the response.

This assumes an empty command-line project targeting .NET 6 or newer.

### Installation
The two packages [`DragonFruit.Data`](https://nuget.org/packages/DragonFruit.Data) and (optionally) [`DragonFruit.Data.Roslyn`](https://nuget.org/packages/DragonFruit.Data.Roslyn) can be installed from NuGet via `<PackageReference>` tags in a `csproj` file or through your preferred GUI.

### Create a Client
An `ApiClient<T>` needs to be created somewhere visible to everything that will access it, for example as a static property (or Singleton instance if using a dependency-injection framework)

The <T> represents the default serializer used for classes that don't have a specific serializer chosen for them. There are two default serializers that are provided by default: `ApiJsonSerializer`
and `ApiXmlSerializer`.

In the example `Program.cs` file below an internally accessable client is created `Program.Client`:

```cs
using System.Threading.Tasks;
using DragonFruit.Data;
using DragonFruit.Data.Serializers;

namespace DataExample;

public class Program 
{
    internal static ApiClient Client = new ApiClient<ApiJsonSerializer>
    {
        UserAgent = "DataExample"
    };

    public static async Task Main(string[] args)
    {
        // main app logic goes here...
    }
}
```

### Create a request
Next we need model a request to send.

In this example, we want to contact the Steam API for news about a specific game. We can create a class inheriting from `ApiRequest` with the parameters (the game id, number of items, etc.) defined as properties:

```cs
using DragonFruit.Data;
using DragonFruit.Data.Requests;

namespace DataExample;

public partial class SteamNewsRequest : ApiRequest
{
    public override string RequestPath => "https://api.steampowered.com/ISteamNews/GetNewsForApp/v0002";

    public SteamNewsRequest(int appId)
    {
        AppId = appId;
    }

    [RequestParameter(ParameterType.Query, "appid")]
    public int AppId { get; set; }

    [RequestParameter(ParameterType.Query, "count")]
    public int? Count { get; set; }

    [RequestParameter(ParameterType.Query, "maxlength")]
    public int? MaxLength { get; set; }

    [RequestParameter(ParameterType.Query, "format")]
    protected string Format => "json";
}
```

In this example, a `SteamNewsRequest` requires an `AppId`, but `Count` and `MaxLength` are optional. If they are not set (`null`) they will not be included in the request.

The class is marked as `partial` to allow the source generator to pre-compute the procedure needed to take the request and build it for the client to send. See [Requests](/wiki/rest-client/requests) for more examples.

### Perform the request and get the output
After the client has been created and a request has been defined, we can make the request. Updating the `Main` method from `Program.cs`, we can now get some data back:

```cs
public static async Task Main(string[] args)
{
    var tf2NewsRequest = new SteamNewsRequest(440);
    var tf2News = await Client.PerformAsync<JsonObject>(tf2NewsRequest);

    // in this example we didn't define a set of classes to model the response, you can replace JsonObject with the response class type to deserialize directly.
    var latestArticleTitle = tf2News["appnews"]["newsitems"][0]["title"].GetValue<string>();
}
```

### Conclusion
This is only a very basic demonstration of what the library can do. Refer to the additional documents to see more features of the library including:

- Sending other types of requests with complex data
- Downloading files with modification date checks
- Customising the client
- Creating custom serializers
