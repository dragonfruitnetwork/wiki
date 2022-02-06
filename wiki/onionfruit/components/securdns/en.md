# SecurDNS

OnionFruit™ DNS Routing (also known as SecurDNS) was introduced in the 2021.116 update, allowing DNS queries to be resolved through Tor.

> There are known issues with Windows 11. See [this issue](https://github.com/dragonfruitnetwork/onionfruit/issues/22) for more details

This enables a Tor feature allowing `.onion` sited to be mapped locally, where the Tor client can then perform the request to the correct server.
While this now allows for dark-net sites to be viewed inside a normal browser, **it is strongly discouraged** as trackers and the browser itself could be used to identify you. The Tor browser is a much better alternative if you're actually serious.

### How to use

> Because this changes DNS settings, admin elevation is required. OnionFruit™ will automatically ask for this if it's needed. If denied, the app will continue to function but the feature won't work

1. Make sure you're running 2021.118 or a newer version.
2. Open the Settings page, and navigate to the DNS tab.
3. Toggle the `Enable SecurDNS` switch to the ON position.
4. Add any alternative DNS servers (for IPv4 and IPv6)
5. Click the restart button and connect in the new instance of OnionFruit™

### Notes

- This will replace your DNS settings while the session is active, replacing them with the originals on disconnect.
- Upto 4 fallback servers will be selected. If none are provided, they will default to [CloudFlare's 1.1.1.1 DNS service](https://1.1.1.1/dns/)
- **This is currently experimental**. Don't expect everything to be 100%. We encourage you to open an issue if something isn't working.
- If no Tor-enabled sites are working, try **disabling IPv6** for the network interface used, as some ISPs seem to be unable to get it to work properly.
- **Dark net responsibly**. As per our [disclaimer](../legal/disclaimer), we take no responsibility if you get caught.