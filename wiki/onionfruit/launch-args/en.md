# OnionFruit™ Launch Arguments

The OnionFruit™ client can be launched with a combination of switches to change behaviour. These shouldn't need to be used but they're there for advanced usage or additional diagnostic data is required.

| Switch               | Name      | Description                                                                                                                                                           |
|----------------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -auto                | Autostart | The flag used when Windows autostarts OnionFruit™. Tor is automatically connected and there is no UI except for the notification icon.                                |
| -console             | Console   | Show log output directly in a console window.                                                                                                                         |
| -safe                | Safe      | Currently has no uses?                                                                                                                                                |
| -priority            | Priority  | When running Tor, the processes' priority is increased. As of the 2021.114 update, this became an optional feature in the settings menu.                              |
| -v                   | Verbose   | Enables verbose logging                                                                                                                                               |
| -update or -recovery | Update    | Runs the OnionFruit™ updater at launch. Can be used if you can't get to the main screen to start updating. This will also be tripped on next boot if the app crashes. |