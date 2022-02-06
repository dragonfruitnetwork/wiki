# OnionFruit™ Troubleshooting

> Issues can be filed by email at inbox@dragonfruit.network or on [GitHub](https://github.com/dragonfruitnetwork/onionfruit/issues)

### I have no internet connection after using OnionFruit™
Firstly, don't freak out. First check if you can disable Tor from the toggle inside the OnionFruit™ window. If you've killed the app or that has no effect, open task manager and kill `tor.exe` and `DragonFruit.OnionFruit.Windows.exe`. You can then find the proxy settings (either using the settings app or on older devices the Internet Options) and disable the proxy from there.

If you still have no connection, please open an issue or contact us via email

### Can I connect to Tor through an existing proxy?
No. We have removed this feature due to low usage and some issues discovered when trying to authenticate against proxies that use NTLM/Keberos authentication, like Netsweeper.

### My internet connection is restricted. Can I still use Tor?
If you're using a newer copy of OnionFruit, some settings might be pre-configured. If not, you can try some of the bridge settings to find one that works.

### I've only got "Random" as a country. What's going on?
Please update to the latest version on the GitHub Releases. There was an issue with the previous Tor information provider and have converted to use an in-house system instead.

### OnionFruit™ stays that Tor is disabled and I can't connect
OnionFruit™ performs checks including a file verification and a registry test, to make sure OnionFruit™ can connect to Tor and alter proxy settings properly. If **any** of these checks were to fail, the app will refuse to connect to Tor. 

### Can I use this at work or school to bypass filtering restrictions?
Not really. Filtering providers such as Netsweeper use proxies that require NTLM logins, something OnionFruit™ and Tor no longer supports.

### Crashes
If the app has crashed, it is likely we have been sent a report with all the info we need to fix it. If you wish to send us additional information, feel free to create an issue on the OnionFruit GitHub repo, providing as much info as possible.

***

## Older Windows Bugs (7 and 8.1)
> If you are running OnionFruit™ on an unsupported platform, these are the only fixes we will give. If you have an error, find it in Event Viewer, search the error online and see if you can fix it **before** contacting us.

### `CLR20r3` Error
The CLR20r3 Error can be caused by Windows or .NET Framework. Potential fixes include:

* Upgrade to Windows 10
* Reinstall .NET Framework
* Update .NET Framework to 4.7.2 or 4.8
* Changing Display Language to English (en-US or en-GB)
