# Dragon6 Desktop
_previously known as Dragon6 Electron_

Dragon6 Desktop is a Windows edition of Dragon6 web, with support for additional features including news feeds, saved players, recent players, more stats and faster loading times.

The client can be downloaded on compatible Windows devices from the [Microsoft Store](https://www.microsoft.com/en-gb/p/dragon6/9n88cqpkgs15)

### History

<!-- todo add link to Orbit when released -->

Dragon6 Desktop was initially released in February 2019 as a WPF app, which was replaced a few months later with a client that closer matched the website (bundled as an [Electron app](https://www.electronjs.org/)). In March 2021, the Electron backend was replaced in favour of a WebView2-backed system maintained in-house by the DragonFruit development team. It shares most of its code with the Orbit implementation, with the most notable changes including the omission of update checking at startup and a different colour scheme.

### Trivia
- When downloading the Dragon6 desktop app, Windows 11 users will have a significantly smaller download and disk footprint due to [Windows bundling WebView2](https://blogs.windows.com/windowsdeveloper/2021/10/04/developing-for-windows-11/) with new versions of Windows