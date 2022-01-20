# Levels and Lootboxes
_for Dragon6-issued levels, refer to [verification](../verification)_

Dragon6 offers the option to fetch the player's clearance level and lootbox (alpha pack) chances. This is done with a single api call, and can be done for multiple accounts at once. While these endpoints are still active and updated, they are namespaced under `Legacy` because of similarities between other depreciated endpoints.

### Usage
```cs
var accountLevel = await client.GetLegacyLevelAsync(account).ConfigureAwait(false);
```