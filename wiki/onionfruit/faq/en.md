# OnionFruit™ FAQ

Below you'll find some common questions and their answers. If we've missed something, create an issue and we'll get back to you ASAP

## Can I connect using any app?
Yes, providing the app you want to use is capable of using SOCKS5 and is set to use the system proxy, it shouldn't be an issue.

## Can I connect to .onion sites
If you have version 2021.116 (which is on cutting edge), you can enable the SecurDNS feature which will allow any app to resolve `.onion` sites. This requires admin privileges and is currently an experimental feature. There are also issues when running on Windows 11.

For more information, see the [DNS routing page](/wiki/onionfruit/components/securdns)

## Do you have a portable copy?
No, because the installer uses Squirrel, you don't need admin rights to install/use it. If you still need a portable copy then it's highly likely the target machine you're trying to use won't allow the program to change the appropriate settings.

## The app keeps crashing. What do I do.
First, try rebooting. You'd be surprised how many issues can be fixed like that.
If it keeps crashing, head to `%localappdata%\DragonFruit Network\OnionFruit\Logs` and open the more recent logs. If you find some entries with ERR/WRN they should tell you what's happening. If it's 100% out of your control, open an issue with the logs attached and we'll look into a fix. If the error occurs before the updater would have fired (i.e before the connect window shows), you will need to uninstall and install the latest copy.

## What data do you collect?
The only data we collect are crash reports, compromised of the .NET Framework Version, Windows Version and the last 25/50 lines of the log before the error occurred. At the moment you cannot turn this off due to an issue in the startup section, resulting in the setting taking no effect.

## Some 3rd party sites say it's ad-supported or open-source?
It **was previously** open source, but that was when the code was in a very raw state. We now use multiple proprietary libraries and as a result, have been forced to go closed-source.

For a **1-week period in 2017**, we made some changes to the app to redirect to an ad-supported site. This change is no longer present. We've also made some modifications to our site over the years, and you can now enjoy a modern, cleaner and faster site.