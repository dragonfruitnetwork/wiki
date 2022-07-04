---
tags:
  - discord
  - bot
---

# Dragon6 Discord

Dragon6 offers a Discord bot that can be used to access stats within the Discord chat interface. The bot can be invited using the link on the [Dragon6 website](https://dragon6.dragonfruit.network/discord)

## Using the bot

After inviting the bot using the link above, it's ready to use. We recommend setting a couple of dedicated channels for commands to be sent from to prevent over-cluttering, which can be done by visiting your [server's integrations page](https://support.discord.com/hc/en-us/articles/360045093012-Server-Integrations-Page).

> Admins of a server can use all slash commands in any text channel, regardless of restrictions applied in the integrations page

Commands are invoked by typing a forward slash (`/`), followed by the command name and any options required. Some commands may require more information than others - the table below outlines each command, its options and expected response.

## Commands

Command options in [square brackets] denote the option is required, while options surrounded by (curved brackets) are optional

### `/about [username] (platform)`

Gets basic information about an account including:

- Time since last gameplay session
- Number of gameplay sessions
- Date the game was first played

### `/level [username] (platform)`

Gets the level and alpha pack chances of the provided user.

### `/overview [username] (platform)`

Fetches and displays a general overview of the user's gameplay over the past ~60 days. Stats are aggregated from Casual, Ranked and Unranked gameplay.

### `/seasonal [board] [username] (platform)`

Fetches the user's seasonal stats for the provided leaderboard (ranked, casual or deathmatch). The user must have played (or abandoned) at least one match for the command to return any meaningful response.

### `/operators [username] (platform)`

Displays the players most picked operators from the past ~60 days across casual, unranked and ranked

### `/players`

Displays the number of players currently online who own the game through Steam

### `/dragon6-apps`

Returns a set of links to other Dragon6 apps (only the caller can view the response)

## Trivia

- The platform parameter is not needed unless the user is not on PC/UPlay
- Linking a Discord account from the Dragon6 website allows callers to substitute the `username` option to `me`
- Most errors are returned as [ephemeral messages](https://support.discord.com/hc/en-us/articles/1500000580222-Ephemeral-Messages-FAQ), meaning they will expire and others cannot view them
