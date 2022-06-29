# Getting Started
> Applies to library version **2020.0730.9-beta** and higher

### Create a project and add Dragon6

1. If you haven't already, create a c# project in Visual Studio, Rider or whatever IDE you're using that targets .NET Core 3.1 or higher.
2. Once you've created it, right click the project in the Solution explorer and click `Manage Nuget Packages`
3. (On Visual Studio, click Browse first) then type into the search box `DragonFruit.Six.Api`
4. Select the one by DragonFruit Network and click the plus button/install button that shows. **Make sure the version you're installing is equal to or higher than the version stated above** - if it isn't check the `enable prerelease versions` box to view all entries

### Create the stats client
You now need to decide how you want to cache access tokens. This is important as when debugging, you'll likely restart the app multiple times which will run your login quota dry quickly. We recommend storing the token in a text file and try to retrieve it from there before resorting to online measures. In production, you could consider using other providers such as Redis, or a NoSQL database to store the token instead.

To create a stats client, add a new class that inherits `Dragon6Client` and implement the function `GetToken`. A single instance should then be initialised for the duration of the session, either marking it as `static` or using a dependency container with a `Singleton` lifetime (or equivalent).

See the "Usage" section in [Clients](/wiki/dragon6/developers/clients) to see an example of how to implement the client.

### Use the client
When accessing the client, the library provides a set of extension methods to get developers started as soon as possible. Refer to the [Dragon6 Developer homepage](/wiki/dragon6/developers) for specific aspects of the library and examples.