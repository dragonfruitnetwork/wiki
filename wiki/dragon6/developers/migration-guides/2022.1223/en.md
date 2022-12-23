# DragonFruit.Six.Api Migration Guide 2022.1223

This is a migration guide listing the biggest breaking changes to the library that developers should pay attention to.

### 🗑️ Removal of account activity methods
Ubisoft has stopped updating the times users has last logged into the game, and as it doesn't look like it's getting unblocked soon we've removed the ability to access the data.

### ⚠️ Changes to Authentication
Because of the way authentication is managed on some of the APIs used internally to fetch data, tokens from multiple sources may need to be used - for example, the Ranked2 endpoints need to be authenticated as the game itself, but the token used to load those stats cannot be used to get some stats on other platforms.

In response to adding the new endpoints, the way tokens are fetched has been changed to accompodate some endpoints requring specific service tokens:

- The `SetUbiAppId()` method has been removed, and has been replaced with the `DefaultService` property
- The `GetToken()` method now accepts both a `UbisoftService` and `string` parameters

  ```cs
  // old
  protected override Task<IUbisoftToken> GetToken(string sessionId) { }

  // new
  protected override Task<IUbisoftToken> GetToken(UbisoftService service, string sessionId) { }
  ```

### 🌱 Removal of legacy levels and introduction of cross-platform levels
The old levels API has been removed due to levels not reflecting potential cross-platform changes, and has been replaced with a cross-platform compatible alternative.

There are a couple of differences with this endpoint:

- It's not batch-lookup compatible
- It doesn't return alpha-pack chances unlike the previous endpoint

```cs
// old
var level = await client.GetLegacyLevelAsync(account).ConfigureAwait(false);

// new
var level = await client.GetAccountLevelAsync(account).ConfigureAwait(false);
```
