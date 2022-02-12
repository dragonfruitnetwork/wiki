# Ubisoft Account API
Ubisoft provides a set of endpoints that can be used to lookup general account information, including reverse-id searching.

| Property   | Description                                                                                                      |
|------------|------------------------------------------------------------------------------------------------------------------|
| Username   |                                                                                                                  |
| Platform   | The platform the user was looked up on                                                                           |
| Image      | A url for the user's avatar image (256x256px)                                                                    |
| ProfileId  | The id used to return stats. This is not always the same as the other identifiers                                |
| UbisoftId  | The id of the Ubisoft account. Can be used in conjunction with the Platform to get a user's current account info |
| PlatformId | The id of the user on the original platform                                                                      |

### Usage
> This assumes you have created a custom [Dragon6Client](../clients)

```cs
private async Task GetAccountInfo(string identifier, Platform platform)
{
    // NOTE: you can also run GetAccountsAsync instead and pass a load of identifiers to get back
    var accInfo = await Client.GetAccountAsync(identifier, platform, IdentifierType.UserId).ConfigureAwait(false);

    // for the account, get their activity on R6
    var loginData = await Client.GetAccountActivityAsync(accInfo).ConfigureAwait(false);
}
```