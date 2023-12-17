# DragonFruit REST Client

[![Latest Nuget](https://img.shields.io/nuget/v/DragonFruit.Data?label=DragonFruit.Data&logo=nuget)](https://nuget.org/packages/DragonFruit.Data)
[![Latest Nuget](https://img.shields.io/nuget/v/DragonFruit.Data.Roslyn?label=DragonFruit.Data&logo=nuget)](https://nuget.org/packages/DragonFruit.Data.Roslyn)

### Overview

DragonFruit.Data is a HTTP REST client for .NET that is designed to be easy to use and acts as the main web communication system for many DragonFruit products, including internal tools.

The design of the system is focused on three main components:

- **Requests** modeled from a REST/HTTP service, defining queries, forms, bodies and headers to be sent
- **Clients** that are responsible for taking requests and sending them to their destination
- **Serializers** that transfer objects between the client and server

Additionally, the optional source generator can be used to improve runtime performance by pre-generating the request building logic at compile time instead of using reflection at run-time.

### Table of Contents

| Page                                                                | Description                                                              |
|---------------------------------------------------------------------|--------------------------------------------------------------------------|
| [Getting Started](/wiki/rest-client/getting-started  )              | A quick guide for getting started                                        |
