# Ovrlord - Coming soon...


Ovrlord is a monolithic personal media library system that manages collections of digital media assets such as **Movies** and **TV Series**.

The system must support multiple libraries, flexible storage configurations, quality evaluation, and full traceability from request to acquired media.

The system should be designed for **future extensibility** to support additional media types such as Music or Audiobooks.

## Features

- **Unified Control** - Centralize all your media in one powerful, monolithic system designed for complete oversight
- **Integrated Search & Download** - Seamlessly discover and acquire new content with built-in search and automated download capabilities.
- **Request Management** - Streamlined request handling system that lets you manage and fulfill content requests effortlessly.
- **Dual Authentication** - Support for both password and OIDC authentication
- **Content Filtering** - Blacklist content by age rating, genre, or individual items
- **User Management** - Invite system, user roles, and permissions

## Why yet another Arr inspired application?

Existing *Arr tools are well-established and battle-tested, but they are fundamentally discrete applications — each scoped to a specific task or media type. Managing a complete media stack typically means running and maintaining several of these applications in tandem. This fragmentation increases the complexity of initial setup, ongoing configuration, and long-term maintenance.

Ovrlord's primary goal is to eliminate that friction by consolidating media management into a single, cohesive system. One application. One configuration. One place to manage your entire library.

Beyond simplification, existing tools carry architectural constraints that surface as real-world limitations. Maintaining both HD and UHD copies of the same movie typically requires running two separate instances of an application. Edition support is often an afterthought rather than a first-class concept.

Ovrlord is designed from the ground up to address these gaps:

- **Multiple libraries**, each with independent storage layouts and naming templates per media type
- **Multiple copies of the same media**, natively differentiated by Quality Profile and Edition
- **Deterministic quality scoring** via Custom Formats, giving precise control over which copy is preferred
- **Full acquisition traceability** — every file can be traced back to the originating request, indexer result, and acquisition event
- **Future extensibility** for additional media types such as Music and Audiobooks, without requiring separate applications

The goal is not to replace the *Arr ecosystem overnight, but to offer a simpler, more unified path for those who want complete oversight of their media library without the operational overhead of managing a fleet of services.

## Guides & Documentation

- [High Level Feature Requirements](docs/REQUIREMENTS.md)

## 🤖 AI-Free by Design

Ovrlord is intentionally built without any AI driven features. We believe it is not ideal for a self-hosted local media collection application to require AI to function.  Therefore, we will not be accepting any issue requests or pull requests for AI driven features.

## Quick Start

### Prerequisites

- PostgreSQL 18+
- TMDB API key - used to fetch movie and series details like title, imagery
- Usenet Indexer(s) - to search for media releases
- Usenet Provider(s) - to download indexer articles

## License

This project is licensed under the GNUv3 - see the [LICENSE](LICENSE) file for details.

## Support

- 🐛 [Issues](https://github.com/ovrlord-app/ovrlord/issues)
