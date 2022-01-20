# Legacy Stats
Dragon6 API offers access to the stats used by the official website prior to September 2020. These include:

### Mode and Playlist stats
Classic stats such as overall kills/deaths, wins/losses and time played are available for all modes (Casual and Unranked, Ranked, Training) and rulesets (Secure, Bomb, Hostage)

```cs
var generalStats = await client.GetLegacyStatsAsync(account).ConfigureAwait(false);

generalStats.Casual.Kills; // get the casual kills
generalStats.Hostage.Wins; // get wins on hostage mode
generalStats.Barricades; // get total barricades deployed
```

### Weapons
Weapon stats are returned in an `IEnumerable<LegacyWeaponStats>` type containing the weapon class, kills, picks, headshots and some accuracy metrics

```cs
var weaponStats = await client.GetLegacyWeaponStatsAsync(account).ConfigureAwait(false);

foreach(var weapon in weaponStats)
{
    weapon.Class; // get the weapon type (as an enum)
    weapon.Kills; // get the kills for this weapon class
}
```

### Operators
Operator stats (pre Y6S4) are included with kills, deaths, wins, losses, time played, experience gained and headshot count. In order to get metadata for the operators (name, attack/defender, organisation), the Dragon6 dataset can be fetched and left or inner-joined against the stats to get a complete list of stats

```cs
var operatorInfo = await client.GetLegacyOperatorInfoAsync().ConfigureAwait(false);
var operators = await client.GetLegacyOperatorStatsAsync(account).ConfigureAwait(false);

// this combines both operator info and stats into a Tuple<LegacyOperatorInfo, LegacyOperatorStats>
var stats = operatorInfo.Join(operators, i => i.OperatorId, s => s.OperatorId, (i, s) => Tuple.Create(i, s)).ToArray();

foreach(var (operatorInfo, operatorStats) in stats)
{
    operatorInfo.Name; // get the name of the operator
    operatorStats.Kills; // get the operator killcount
}
```