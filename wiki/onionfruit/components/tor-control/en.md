# OnionFruit™ RPC Console

Advanced Tor users can use the built-in Tor Control interface to send and receive information about the current state of the Tor client process. This was introduced in the [2021.415 update](https://dragonfruit.network/changelogs/onionfruit/2021.415).

### Accessing the console

After connecting to Tor through the client, right-click the window and select `Tor Control`. A window should show that says ```authenticating... 250 OK```, at which point you can then use the message box at the bottom of the screen to send a command to the Tor process.

### Notes
- **This is experimental** and could break or change between updates. Suggestions should be opened as issues on this GitHub repo.
- **The port is password protected** with a randomly generated password on each connection. This is to protect against other programs/users interacting with it, potentially causing instability within OnionFruit™ itself
- The autosuggest list is not exhaustive. It's merely there for suggestions.
- Some commands will be filtered and dropped. This is because some settings collide with what OnionFruit™ sets at start (mainly ports) and some commands can cause the program to become unstable