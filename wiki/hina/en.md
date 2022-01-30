# DragonFruit Identity System

The DragonFruit Identity service (also known by its internal codename, `hina`), is a platform used to allow designed to allow DragonFruit-developed services to integrate single-sign-on (SSO) login. It allows users to login with one of the following providers:

- DragonFruit (internal)
- Microsoft
- Google
- GitHub
- Discord
- Steam

Users will have a DragonFruit id created on signing in with an account that has not been previously associated. After signing in, visiting the [site](https://id.dragonfruit.network) will allow users to link multiple 3rd party providers to a single DragonFruit id, allowing user signins from any of the accounts. Any account added after the first one can be removed from the id.

> Information such as your name and email can be changed once logged in

### Clients
_also referred to as apps_

Users can create clients to interact with services including the Dragon6 API and perform delegate actions (actions that operate on the owner's behalf as a user). Some clients are interactive and can retrieve user information. These are only created by DragonFruit for official means and are unavailable to other users.

Any service you login to does not know what provider you have used, and you will be given the chance to review the data each client has requested. 