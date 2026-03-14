# Process Flows

This document describes the common process flow paths within Ovrlord, covering request handling, acquisition, upgrades, manual operations, and scheduled background jobs.

## Table of Contents

- [Request Flow](#request-flow)
  - [Auto-Approved Request](#auto-approved-request)
  - [Manually Reviewed Request](#manually-reviewed-request)
- [Acquisition Flow](#acquisition-flow)
        - [Manual Acquisition (Admin-Initiated)](#manual-acquisition-admin-initiated)
- [Upgrade Flow](#upgrade-flow)
- [RSS Feed Flow](#rss-feed-flow)

---

## Request Flow

A Request begins when a user submits a request for a specific media item, specifying a target library, edition, and quality profile. The system then determines whether the request requires admin review or can be automatically approved.

### Auto-Approved Request

Applies when auto-approval is enabled at the **user level** or **global level**.

```
User submits Request
        │
        ▼
System checks auto-approval setting
(user-level OR global-level)
        │
        ▼ [Auto-approval enabled]
Request status set to: Approved
        │
        ▼
[Acquisition Flow begins]
```

### Manually Reviewed Request

Applies when auto-approval is **not** enabled for the requesting user and no global override is active.

```
User submits Request
        │
        ▼
System checks auto-approval setting
(user-level OR global-level)
        │
        ▼ [Auto-approval disabled]
Request status set to: Pending Review
        │
        ▼
Admin reviews Request
        │
        ├── [Rejected] ──► Request status set to: Rejected
        │                   Requesting user notified
        │
        └── [Approved] ──► Request status set to: Approved
                            │
                            ▼
                    [Acquisition Flow begins]
```

---

## Acquisition Flow

Triggered immediately after a Request is approved, whether by auto-approval or admin action.

```
Request Approved
        │
        ▼
Media item added to library as Monitored
with selected:
  - Target Library
  - Edition
  - Quality Profile
        │
        ▼
Indexer Search triggered automatically
        │
        ▼
Search results collected from configured Indexers
        │
        ▼
Each result scored against the selected Quality Profile
using Custom Format scoring rules
        │
        ▼
Highest-scoring result selected
        │
        ├── [No results meet Quality Profile criteria]
        │       Media remains Monitored, awaiting future
        │       search (RSS or scheduled upgrade check)
        │
        └── [Qualifying result found]
                │
                ▼
        Release sent to Download Queue
                │
                ▼
        Download completes
                │
                ▼
        Media file imported into library
        Acquisition event recorded for traceability:
          - Originating Request
          - Indexer search result
          - Acquisition event timestamp
```

---

### Manual Acquisition (Admin-Initiated)

Admins may bypass scheduled automation and initiate acquisition actions directly.

```
Admin initiates Manual Indexer Search for a media item
        │
        ▼
System queries configured Indexers
        │
        ▼
Raw search results returned and displayed to Admin
        │
        ▼
Admin reviews results and selects specific release(s)
        │
        ▼
Selected release sent to Download Queue
        │
        ▼
Download completes, media imported into library
```

---

## Upgrade Flow

Runs on a **scheduled cadence** to identify whether any monitored media item can be replaced with a higher-quality copy.

```
Scheduled Upgrade Job triggered
        │
        ▼
For each Monitored media item in library:
        │
        ▼
Retrieve current media file's Custom Format score
        │
        ▼
Query configured Indexers for new results
        │
        ▼
Score each result against the item's Quality Profile
        │
        ├── [No result scores higher than current file]
        │       No action taken, item remains unchanged
        │
        └── [Higher-scoring result found]
                │
                ▼
        Release sent to Download Queue
                │
                ▼
        Download completes
                │
                ▼
        New file imported, replaces previous copy
        Upgrade event recorded for traceability
```

---

## RSS Feed Flow

Runs on a **scheduled cadence** to discover newly released media published to configured Indexer RSS feeds.

```
Scheduled RSS Feed Job triggered
        │
        ▼
Fetch latest entries from configured Indexer RSS feeds
        │
        ▼
For each RSS entry:
        │
        ▼
Match entry against Monitored media items in library
        │
        ├── [No match found]
        │       Entry ignored
        │
        └── [Match found]
                │
                ▼
        Score entry against matched item's Quality Profile
                │
                ├── [Score does not improve on existing file]
                │       Entry ignored
                │
                └── [Score improves on existing file OR
                     item has no file yet]
                            │
                            ▼
                    Release sent to Download Queue
                            │
                            ▼
                    Download completes, media imported
                    into library (or replaces existing file)
```
