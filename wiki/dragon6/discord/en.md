---
tags:
    - discord
    - bot
---

# Dragon6 Discord

Dragon6 offers a Discord bot that can be used to access stats within the Discord chat interface.

## Inviting the bot
The invite link can be found on the [Dragon6 website](https://dragon6.dragonfruit.network/discord)

## Using the bot
It is recommended the bot is given a dedicated channel in your server to prevent over-cluttering. We _strongly_ recommend rate-limiting the channel in addition to prevent hard rate-limits being hit often. Most commands are ratelimited to 1 command every 5 seconds (per user across all servers). The bot does **not** accept DMs and will not respond to them.

The bot is addressed by mentioning the bot `@Dragon6` (when typing), or `<@679701260177244163>` (copy-paste) followed by the command (see table below)

### Commands

- `help` - display the welcome message with commands list
- `support` - get a link to the DragonFruit Discord
- `players` - get the current number of players on Rainbow Six (for Steam platform only)
- `about [username] (platform)` - gets info (last login date and session count) about the requested user
- `stats [username] (platform)` - gets general stats (overall stats) for the requested user
- `casual [username] (platform)` - gets casual stats (K/D, W/L, MMR) for the requested user for the current season (casual)
- `ranked [username] (platform)` - gets casual stats (K/D, W/L, Rank) for the requested user for the current season (ranked)

### Notes
- When a username contains whitespace, it must be surrounded by double quotes (e.g. `"a username with spaces inside"`)
- The platform parameter is not needed unless the user is not on PC/UPlay