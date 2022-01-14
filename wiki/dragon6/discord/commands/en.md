---
tags:
    - bot
    - discord
    - commands
---

# Dragon6 Discord Bot Commands
The Dragon6 bot supports a large array of commands which can be used to lookup user stats, accounts, activity and even how many people are online at the current point in time.

### Commands
> The bot is addressed by prefixing the message with `@Dragon6` (when typing), or `<@679701260177244163>`.

- `help` - display the welcome message with commands list
- `support` - get a link to the DragonFruit Discord
- `players` - get the current number of players on Rainbow Six (for Steam platform only)
- `about [username] (platform)` - gets info (last login date and session count) about the requested user
- `stats [username] (platform)` - gets general stats (overall stats) for the requested user
- `casual [username] (platform)` - gets casual stats (kd, wl, MMR) for the requested user for the current season (casual)
- `ranked [username] (platform)` - gets casual stats (kd, wl, MMR) for the requested user for the current season (ranked)

### Notes

- If a `[username]` has a space in it, it needs to be surrounded by double-quotes if not on PC (like `about "A long username" XBL`)
- Commands with square bracket parameters are **required**, and curved brackets are **optional**