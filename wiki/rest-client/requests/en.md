# Writing Requests
Writing requests is the primary purpose of the REST framework. The DragonFruit.Data `ApiRequest` allows users to design requests that utilise query strings, different body types, custom headers and callbacks while providing ease-of-use and the ability to fully document requests.

Originally, DragonFruit.Data would use reflection to get properties and build the request, in v4 the request building engine has been redesigned to be more resource efficient and introduces the source generation package, `DragonFruit.Data.Roslyn` that eliminates the runtime cost of reflection and provides consistency when deploying a project on different platforms (i.e. Windows and Android) where reflection methods may differ.

## Supported Types
`ApiRequest` builders are flexible and supported types include:

- Strings
- `IEnumerable`
- `enum` types
- Primitives (`int`, `long`, `byte`, `bool`, etc.)
- Nullables (`int?`, `long?`, `byte?`, `bool?`, etc.)
- `IEnumerable<KeyValuePair<string, string>>`

Additionally, when sending POST requests in a class decorated with `[FormBodyType(FormBodyType.Multipart)]` additional types are supported:

- `byte[]`
- `Stream`
- `HttpContent`

Types not covered in this list (structs, classes) will use the `.ToString()` implementation provided which may result in unintended behaviour.

## Important Notes
- `ApiRequest` classes should be marked as `partial` if the source generator will be used. Failure to do so will result in compilation errors
- Properties should not be `private` or `internal` as these can break the source generators and prevents extending requests if they're compiled into a library
- Type constraints for bodies should be restricted to `class` to allow serialization to work properly

## Features
> This section assumes a basic understanding of how to create an `ApiRequest`. Refer to the [Getting Started](/wiki/rest-client/getting-started) guide to learn how.

### Sending different request types
`ApiRequest` exposes a virtual property that allows the request method (`GET`, `POST`, `PATCH`, etc.) to be changed:

```cs
public partial class MethodTypeRequest : ApiRequest
{
    public string RequestPath => "https://example.com";

    // override the method to PATCH
    public override HttpMethod RequestMethod => HttpMethod.Patch;
}
```

### Send form contents in a request
Adding properties that are decorated with `[RequestParameter(ParameterType.Form, "name")]` allows them to be included in a form body content. By default, the generator will use the `application/x-www-form-urlencoded` type but can be customised with the `FormBodyTypeAttribute`:

```cs
[FormBodyType(FormBodyType.Multipart)] // send a multipart request
public partial class PostRequest : ApiRequest
{
    public string RequestPath => "https://example.com";

    public override HttpMethod RequestMethod => HttpMethod.Post;

    [RequestParameter(ParameterType.Form, "u")]
    public string User { get; set; }

    [RequestParameter(ParameterType.Form, "comment_text")]
    public string Comment { get; set; }
}
```

### Send a request with a custom body
Requests that need to send a serialized body, or have a `HttpContent` type that can be sent can provide it via a property decorated with the `[RequestBody]` attribute:

```cs
public partial class PostBodyRequest : ApiRequest
{
    public string RequestPath => "https://example.com";

    public override HttpMethod RequestMethod => HttpMethod.Post;

    [RequestBody] // mark the CommentBody as the request content. because CommentBody does not inherit HttpContent, it will be serialized by the client.
    public CommentBody Comment { get; set; }
}
```

When using this with generic type constraints, **the type must be a class (`<T> where T : class`) otherwise source generation will fail**.

### Add generic parameters with keys that are unknown at runtime
If a request needs parameters that are not known ahead-of-time, `IEnumerable<KeyValuePair<string, string>>` can be used to feed pairs to the request.
This is useful in scenarios where in order to paginate, some key-value pairs need to be returned to the server.

```cs
public partial class PaginationRequest : ApiRequest
{
    public string RequestPath => "https://example.com/pages";

    // place pagination cursor in query
    // IDictionary<string, string> implements IEnumerable<KeyValuePair<string, string>> so can be used.
    [RequestParameter(ParameterType.Query, null)]
    public IDictionary<string, string> Cursor { get; set; }
}
```

### Send enumerables or enums in a request
`IEnumerable` and `Enum` types can be sent in requests:

```cs
public partial class ExtraRequest : ApiRequest
{
    // write collection of strings to query under "ids"
    [RequestParameter(ParameterType.Query, "ids")]
    // concatenated so (ids=a,b,c...)
    [EnumerableOptions(EnumerableOption.Concatenated)]
    public IEnumerable<string> Ids { get; set; }

    // write enum IdType under "type"
    [RequestParameter(ParameterType.Query, "type")]
    // convert enum to numeric represenation (type=1)
    [EnumOptions(EnumOption.Numeric)]
    public IdType EnumOption { get; set; }
}
```
