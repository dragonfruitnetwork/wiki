# Dragon6 Client

### Overview
Dragon6 is built on [DragonFruit.Data](https://github.com/dragonfruitnetwork/dragonfruit.common), a framework which is used across all DragonFruit APIs to enable consistency when working with multiple wrappers in the same project. Due to how Ubisoft authentication works, developers must inherit the base `Dragon6Client` class and provide a way for the client to obtain a token. It is recommended that some form of persistent storage is used to hold tokens due to strict ratelimits imposed on logins, and requesting too frequently can result in a tempoary IP ban.

These clients are designed to be either `static` or `Singleton` (if using a dependency container system), and all client management is automatic, with performance and memory optimisations out-the-box.

### Example
> It is bad practise to store credentials in plain code. These should be stored in a credential manager or environment variables

```cs
using System;
using System.Collections.Generic;
using System.IO;
using System.Net;
using DragonFruit.Data.Serializers.Newtonsoft;
using DragonFruit.Six.Api;
using DragonFruit.Six.Api.Authentication;

namespace DragonFruit.Six.Web.Services
{
    public class StatsClient : Dragon6Client
    {
        // change this to whatever you want
        private readonly string _tokenFile = Path.Combine(Path.GetTempPath(), "ubi.token");

        /// <summary>
        /// Tells the Dragon6 Client how to get a token in the case it's restarted or expired
        /// </summary>
        protected override TokenBase GetToken()
        {
            if (File.Exists(_tokenFile))
            {
                // if we have a file with some potentially valid keys, try that first
                var token = FileServices.ReadFile<UbisoftToken>(_tokenFile);

                if (!token.Expired)
                    return token;
            }

            // store logins somewhere that is NOT in the code
            var username = "username";
            var password = "password";
            var newToken = this.GetUbiToken(username, password);

            // write new token to disk async (non-blocking)
            _ = Task.Run(() => FileServices.WriteFile(_tokenFile, newToken));
            
            // return to keep going
            return newToken;
        }
    }
}
```