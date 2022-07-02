# Dragon6 Client
Dragon6 is built on [DragonFruit.Data](https://github.com/dragonfruitnetwork/dragonfruit-common), a framework which is used across all DragonFruit APIs to enable consistency when working with our libraries. Due to how Ubisoft authentication works, developers must inherit the base `Dragon6Client` class and provide a way for the client to obtain a token. It is recommended that some form of persistent storage is used to hold tokens due to strict ratelimits imposed on logins. **Requesting tokens too frequently can result in a tempoary IP ban. You should save the token recieved to some form of storage (redis, files, etc.)**

These clients are designed to be either `static` or `Singleton` (if using a dependency container system), and all management is automatic, with performance and memory optimisations out-the-box.

As of version [2022.702](https://github.com/dragonfruitnetwork/dragon6-api/releases/tag/2022.702), the `GetToken()` method is fully asynchronous, which improves performance due to networking/IO tasks that occur.

### Example
> It is bad practise to store credentials in plain code. Store them somewhere safe, like a configuration file or environment variables

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
        /// <remarks>
        /// This is a thread-safe method and will not be called more than once at a time, regardless of how many requests the client receives.
        /// </remarks>
        protected override ValueTask<IUbisoftToken> GetToken()
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
            var newToken = await this.GetUbiTokenAsync(username, password).ConfigureAwait(false);

            FileServices.WriteFile(_tokenFile, newToken);
            return newToken;
        }
    }
}
```