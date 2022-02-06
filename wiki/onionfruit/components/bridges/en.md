# OnionFruit™ Bridges

Bridges are a way for people who have restricted/censored internet to be able to circumvent these restrictions by connecting to a non-public guard or through disguising network traffic.

Currently, OnionFruit™ supports 4 types of bridges:

- Unobfuscated (all versions)
- obfs4 (introduced in 2021.415)
- meek (introduced in 2021.415)
- snowflake (introduced in 2021.818)

### Setup

1. Make sure the bridge you want to use is supported and you have the right version of OnionFruit™.
2. Open the settings page
3. Navigate to the "Bridges" tab
4. Enable the bridge option (toggle switch)
5. Select the bridge type and enter the bridge lines if required (as shown on the BridgeDB site or otherwise)

### Notes
- Bridges will override any pre-existing setting relating to Tor input country (from the Tor config tab)
- Bridges can be fetched from the [Tor BridgeDB](https://bridges.torproject.org/options)
- meek and snowflake use public directories and as such, don't need any user-defined bridge lines. They are automatically filled in by the client.