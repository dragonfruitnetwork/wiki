#  Serializers
By default, the `DragonFruit.Data` package comes with two serializers out-of-the-box, `ApiJsonSerializer` and `ApiXmlSerializer`. These use the .NET default serializers and are sufficient for most use cases.

In the event that `Newtonsoft.Json` support is needed, a `DragonFruit.Data.Serializers.Newtonsoft` is provided as an optional package. If this is used the default serializer can be changed to `NewtonsoftJsonSerializer`:

```cs
using DragonFruit.Data;
using DragonFruit.Data.Serializers.Newtonsoft;

public static class Program
{
    internal static ApiClient Client = new ApiClient<NewtonsoftJsonSerializer>();

    public static async Task Main(string[] args)
    {
        // ...
    }
}
```

## Creating a custom serializer
If a custom serializer is desired, one can be created by extending the `ApiSerializer` class. There are a number of properties and methods that require defining:

- `ContentType` - The MIME type of the serialized content (i.e. `text/plain` or `application/json`). This is used in the `Accept` header when requesting a resource that will be deserialized or as the `Content-Type` header that is sent when a request body is serialized.
- `IsGeneric` - if set to `false`, the serializer cannot be used as a default (i.e. as `<T>` in `ApiSerializer<T>`). This is a virtual property and defaults to `true`
- `Serialize<T>(T content) where T : class` - takes an input of type `T` and produces some `HttpContent` that represents it.
- `Deserialize<T>(Stream input) where T : class` - takes an incoming data stream (non-seekable) and deserializes it into an object of type `T`

Additonally, the interface `IAsyncSerializer` can be implemented allowing asynchronous deserialization to take place instead:

- `DeserializeAsync<T>(Stream input) where T : class` - takes an incoming data stream and deserializes it, as part of a potentially asynchronous operation

### Overriding serializers for specific types
Sometimes a serializer may only be used for a small number of types. The `DragonFruit.Data.Serializers.SerializerResolver` class exposes methods to override a serializer used for a given type.

- `Register<T, TSerializer>()` - for type `T`, use `TSerializer`
- `Unregister<T>()` - for type `T`, use the default serializer

Note types used in these methods are only checked as the final type. This means that all inherited types and generic combinations must be declared individually.
