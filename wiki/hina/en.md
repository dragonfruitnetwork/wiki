# DragonFruit Identity System

The DragonFruit Identity service (also known by its internal codename, `hina`), is a platform used to allow users to sign into applicable DragonFruit services and products. It allows users to login with one of the following providers:

- DragonFruit (internal)
- Microsoft
- Google
- GitHub
- Discord
- Steam

Users will create a DragonFruit id on signing in with an account that has not been previously associated. After signing in, visiting the [site](https://id.dragonfruit.network) will allow users to link multiple 3rd party providers to a single DragonFruit id, allowing user signins from any of the accounts.

Any account added after the first one can be removed from the id.

### Clients
Users can create clients to interact with services including the Dragon6 API and delegate actions (actions that operate on the client owner's behalf as a user). Some clients are interactive and can allow logins from other DragonFruit ids. These are only created by DragonFruit for official means and are unavailable to other users.