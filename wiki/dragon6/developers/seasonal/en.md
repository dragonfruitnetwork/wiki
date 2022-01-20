# Seasonal Stats
Dragon6 offers the ability to retrieve seasonal stats for both Casual and Ranked modes with the ability to retrieve previous seasons' data.

#### Season Id
The season id starts at `5`, and increments by one each season. Refer to the [Dragon6 Dataset](https://github.com/dragonfruitnetwork/dragon6-assets/blob/master/public/data/seasons.json) for the season names and metadata. The default value of `-1` will return the current season.

#### Region
Prior to Y5S2, an account could have up-to three ranks based on the region they played in. These regions are:

- `EMEA` - Europe and the Middle East
- `NCSA` - North, Centeral and South America
- `APAC` - Asia and The Pacific

You will need to specify which one you want to return stats for if getting stats prior to season `18`.

#### Playlist
Casual seasonal stats were introduced to the api in Y4S3 (season id `17`) and attempting to retrieve casual stats for a previous season will result in faulure.

#### Ranks
Ranks are automatically calculated based on official rank values and in casual, MMR. These are correct for the season the user played in (for example, a player can achieve Gold 4 in Y3S4, but not now). These can be accessed with the `Rank` and `MMRRank` properties.

### Usage

```cs
var currentSeasonRanked = await client.GetSeasonalStatsAsync(account).ConfigureAwait(false);
var currentSeasonCasual = await client.GetSeasonalStatsAsync(account, board: BoardType.Casual).ConfigureAwait(false);
var previousSeason = await client.GetSeasonalStatsAsync(account, 10).ConfigureAwait(false);
```