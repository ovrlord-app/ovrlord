# High Level Feature Requirements

Ovrlord is a monolithic personal media library system that manages collections of digital media assets such as **Movies** and **TV Series**.

The system must support multiple libraries, flexible storage configurations, quality evaluation, and full traceability from request to acquired media.

The system should be designed for **future extensibility** to support additional media types such as Music, Music Videos, Audiobooks, eBooks, and more.

## Project Goals

- **Unified Control** - Centralize all your media in one powerful, monolithic system designed for complete oversight
- **Integrated Search & Download** - Seamlessly discover and acquire new content with built-in search and automated download capabilities.
- **Request Management** - Streamlined request handling system that lets you manage and fulfill content requests effortlessly.
- **Dual Authentication** - Support for both password and OIDC authentication
- **Content Filtering** - Blacklist content by age rating, genre, or individual items
- **User Management** - Invite system, user roles, and permissions

## Table of Contents

- [Functional Requirements](#functional-requirements)
  - [Media Library Structure](#media-library-structure)
  - [Storage Configuration](#storage-configuration)
  - [Naming Templates](#naming-templates)
  - [Metadata Management](#metadata-management)
  - [Traceability and Provenance](#traceability-and-provenance)
  - [Design Considerations](#design-considerations)
- [Glossary](#glossary)
  - [Media Type](#media-type)
  - [Edition](#edition)
  - [Custom Format](#custom-format)
  - [Quality Profile](#quality-profile)
  - [Upgrade](#upgrade)
  - [Request](#request)

## Functional Requirements

### Media Library Structure

- The system must support **multiple Media Libraries**.
- Each Media Library may contain **multiple Media Types** (e.g., Movies and TV Series).
- A Media Library must allow **multiple copies of the same Movie** when copies differ by:
  - Quality Profile
  - Edition

---

### Storage Configuration

A Media Library must support **configurable root directories per Media Type**.

Example using separate directories:

```
/library/movies
/library/series
```

Example using a shared directory:

```
/library
```

---

#### Naming Templates

Folder and file naming must support **configurable templates**.

Templates must be configurable per:

- Media Library
- Media Type

Example:

- Movie naming templates may differ from TV Series naming templates.

---

### Metadata Management

The system must store metadata for each media item to enable identification, comparison, and scoring.

Required metadata includes (but is not limited to):

- Release Title
- Release Group
- Resolution
- Edition
- File Size
- Runtime
- Custom Format Score

---

### Traceability and Provenance

The system must maintain **traceability for every stored media item**.

Each stored media file must be traceable to:

- The originating **Request**
- The **Indexer search result** that identified the media copy
- The **acquisition event** that added the file to the library

Traceability must support **auditing and debugging of acquisition decisions**.

---

### Design Considerations

The system should prioritize:

- Extensibility for new media types
- Flexible directory layouts
- Deterministic quality scoring
- Full acquisition traceability
- Automated upgrade workflows


## Glossary

### Media Type

A classification of media content.

Supported values:

- `Movie`
- `TV Series`

The system should be designed to support additional types in the future, such as:

- `Music`
- `Audiobook`
- `eBook`
- Other media formats

---

### Edition

A specific version of a media release that differs from the standard version.

Examples:

- Theatrical
- Extended Cut
- Director's Cut
- Unrated

A single media title may have **multiple editions**.

---

### Custom Format

A **scoring model** used to evaluate the desirability of a media file.

The score may consider factors including:

- Scene release naming conventions
- Release group
- Resolution
- File size relative to runtime
- Encoding characteristics
- Other metadata attributes

Custom Format scores are used to determine which copy of a media item is **preferred when multiple copies exist**.

---

### Quality Profile

A configuration defining **acceptable quality criteria** for acquiring media.

Quality Profiles may specify:

- One or more target resolutions (e.g., `720p`, `1080p`, `4K`)
- Acceptable fallback qualities
- Upgrade policies

A lower quality version may initially be acquired and **later upgraded** when a better version becomes available.

---

### Upgrade

The process of replacing an existing media file with another copy that has:

- A **higher Custom Format score**, or
- A **more preferred quality level** defined by the Quality Profile.

---

### Request

A record representing a user request for a specific media item.

A Request must store:

- Requesting user
- Requested media title
- Target Media Library
- Quality Profile used for acquisition

Requests must be **traceable to the acquired media files**.

---