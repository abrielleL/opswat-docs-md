<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/siem-integration -->

# External Loggers — Streaming the MDSS Audit Trail to a SIEM

MetaDefender Storage Security can forward its complete audit trail to a SIEM or log platform in real time — every file scanned with its verdict, every action taken on a blocked file, and every configuration, user and permission change. The feature is called **external loggers**, it is included in the product, and it supports four destination types: Syslog over UDP, Syslog over TCP, Syslog over TCP with TLS, and Apache Kafka.

This page documents the transports, the message formats, every field on the wire, the complete event-type reference, and what the stream does not include.

---

## [1. The short version](/docs/mdss/knowledge-base/siem-integration#1-the-short-version)

| Question | Answer |
| --- | --- |
| Can MDSS integrate with a SIEM? | Yes, over Syslog (UDP, TCP, or TCP with TLS) or Apache Kafka. |
| Is it a separate module or licence? | No. It is included in the product. |
| What is sent? | The complete MDSS audit trail — the same events shown in the console's audit log. |
| How current is it? | Events are sent individually as they happen, typically within a second. |
| Can I send only some events? | Not from MDSS. Every enabled destination receives the whole stream; filter at your collector. |
| How many destinations can I configure? | Five of each type, per tenant. |
| Which permission is needed to configure it? | Write permission on settings. |
| What format are the messages in? | RFC 5424 for Syslog; JSON for Kafka. CEF and LEEF are not produced. |

> **The two things to plan for**
>
> **Volume.** MDSS does not filter server-side, and file-level events dominate the stream. Size the feed and agree a collector-side filter before you enable it — see [section 11](/docs/mdss/knowledge-base/siem-integration#11-filtering-at-the-collector).
>
> **Scope.** External loggers carry the audit trail only. Service and diagnostic logs, API request activity, and failed sign-in attempts are not included — see [section 12](/docs/mdss/knowledge-base/siem-integration#12-not-included-in-the-stream).

---

## [2. What the stream contains](/docs/mdss/knowledge-base/siem-integration#2-what-the-stream-contains)

Every destination receives the same content: the complete MDSS audit trail. That is the same set of events shown under **Audit log** in the console. Nothing is added for external destinations, and nothing is held back.

**Scan activity.** Every file discovered and every file scanned, with the verdict, the reason it was blocked, both hashes, size, path, the storage it came from, the scan that processed it, and the workflow applied. Also scan-level lifecycle events: started, completed, cancelled, failed.

**Post actions.** What MDSS did about each file — moved, copied, deleted, kept, tagged or sanitised — including the destination storage and path for moves and copies.

**Administrative activity.** Storage, group and account changes. Workflow, scan, schedule and remediation changes. User and role changes. Settings changes, including API keys, SSO, TLS certificates, data retention, licence activation, and the external loggers themselves.

**Authentication.** Successful sign-ins and sign-outs.

Failed operations are carried as the same event type at `Error` level rather than as separate event types — a scan that could not complete, a post action that failed, a settings change that was rejected.

---

## [3. How the stream works](/docs/mdss/knowledge-base/siem-integration#3-how-the-stream-works)

MDSS is built from independent services. Each publishes its audit events onto an internal message bus, and a single Logging Service consumes them. For every event, the Logging Service writes to the MDSS audit database and to each enabled external destination in the same operation.

 ┌──────────────────────────────┐
┌─►│ MDSS audit database │
│ │ console audit log · REST API │
│ └──────────────────────────────┘
┌───────────────┐ ┌─────────────┐ ┌────────┴──────┐
│ MDSS services │──►│ Message bus │──►│ Logging │
│ Discovery │ │ internal │ │ Service │ ┌──────────────────────────────┐
│ Scanning │ │ only │ │ adds envelope ├─►│ Syslog destinations │
│ Remediation │ └─────────────┘ │ renders msg │ │ RFC 5424 · UDP, TCP, TCP+TLS │
│ Workflow │ │ writes sinks │ └──────────────────────────────┘
│ Gateway │ └────────┬──────┘
│ Identity │ │ ┌──────────────────────────────┐
│ Licence │ └─►│ Kafka topic │
│ Notification │ │ one JSON object per event │
└───────────────┘ └──────────────────────────────┘

Because the fan-out happens after the audit event is created, the SIEM and the console audit log always describe the same events with the same field values.

### [Delivery semantics](/docs/mdss/knowledge-base/siem-integration#delivery-semantics)

| Aspect | Behaviour |
| --- | --- |
| Ordering | Events are emitted in the order the Logging Service processes them, and each carries an event timestamp and a sortable event id. |
| Latency | Sub-second under normal load. Events are batched — see [section 13](/docs/mdss/knowledge-base/siem-integration#13-limits-and-tuning). |
| Independence | A failure writing to one destination does not affect the others, and never affects the audit database. A slow or unreachable collector never delays a scan. |
| Retry | Best-effort. Events produced while a destination is unreachable are **not** queued for later delivery. They remain in the MDSS audit database. |
| Configuration changes | Applied to the next event. No service restart, no interruption to running scans. |

---

## [4. Supported destinations](/docs/mdss/knowledge-base/siem-integration#4-supported-destinations)

| Destination | `loggerType` | Default port | Payload | Transport security |
| --- | --- | --- | --- | --- |
| Syslog over UDP | `0` | `514` | RFC 5424 | None |
| Apache Kafka | `1` | `9092` (typical) | JSON | PLAINTEXT · SSL · SASL_PLAINTEXT · SASL_SSL |
| Syslog over TCP | `2` | `1468` | RFC 5424 | None |
| Syslog over TCP with TLS | `3` | `6514` | RFC 5424 | TLS, server certificate validated |

Up to **five destinations of each type** may be configured per tenant — five Syslog UDP destinations, five Kafka destinations, and so on. Each is enabled or disabled independently.

### [Syslog options](/docs/mdss/knowledge-base/siem-integration#syslog-options)

| Option | Detail |
| --- | --- |
| Output format | `RFC5424`.The only format offered. CEF and LEEF are not produced. |
| Facility | Any of the 24 standard Syslog facilities, values `0`–`23`, in the usual order from `KernelMessages` to `LocalUse7`. Defaults to `UserLevelMessages` (`1`). |
| Application name | The MDSS product name, sent in the RFC 5424 `APP-NAME` field. |
| Framing | TCP destinations frame each message with CRLF. |

### [Kafka options](/docs/mdss/knowledge-base/siem-integration#kafka-options)

| Option | Detail |
| --- | --- |
| Brokers | Comma-separated `host:port` list. |
| Topic | A single topic name. All events go to it, on any partition. |
| Message key | The event timestamp. Events are not keyed per file or per storage. |
| Security protocol | `PLAINTEXT`, `SSL`, `SASL_PLAINTEXT` or `SASL_SSL`. |
| SASL mechanism | `PLAIN`, `SCRAM-SHA-256` or `SCRAM-SHA-512`, with username and password. |

**Choosing a transport.** Use Kafka if you already operate a broker — events arrive as JSON with named fields, so no log parser is required. Otherwise use Syslog over TCP with TLS. Plain UDP is the least reliable option; see the delivery semantics above.

---

## [5. Configure in the console](/docs/mdss/knowledge-base/siem-integration#5-configure-in-the-console)

Go to **Settings → External loggers**. You need an account with write permission on settings.

1. Select **Add integration** and choose the integration type.
2. For a Syslog destination, enter the server address and port, then choose a facility. The output format is RFC 5424.
3. For Kafka, enter the broker list and topic, then choose the security protocol and — for a SASL protocol — the mechanism, username and password.
4. Save. MDSS tests the connection before storing the configuration. If the test fails, nothing is saved.
5. Use the enable toggle in the list to start or stop delivery at any time without deleting the configuration.

> **Two rules before you save**
>
> A configuration identical to an existing one is rejected as a duplicate. And a connection test must succeed, so the destination has to be reachable from the MDSS deployment at the moment you save — open the firewall first.

---

## [6. Configure over the API](/docs/mdss/knowledge-base/siem-integration#6-configure-over-the-api)

Everything in the console is available on the REST API. The base address is your MDSS console address, for example `https://mdss.example.com/api/`. Authenticate with a bearer token from `/api/user/authenticate` in the `Authorization` header, or with an API key in an `ApiKey` header. All external logger endpoints require write permission on settings.

| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/api/externallogger` | List all configured destinations |
| `POST` | `/api/externallogger/udpSyslog` | Add a Syslog destination (any of the three variants) |
| `PUT` | `/api/externallogger/udpSyslog` | Update a Syslog destination |
| `POST` | `/api/externallogger/kafka` | Add a Kafka destination |
| `PUT` | `/api/externallogger/kafka` | Update a Kafka destination |
| `PUT` | `/api/externallogger/status` | Enable or disable a destination |
| `DELETE` | `/api/externallogger/{id}` | Remove a destination |

### [List destinations](/docs/mdss/knowledge-base/siem-integration#list-destinations)

`GET /api/externallogger` returns every destination for the calling tenant.

{
"entries": [
{
"id": "c9f1e0a4-...",
"isEnabled": true,
"loggerType": 3,
"connectionSettings": {
"serverAddress": "siem.example.com",
"port": 6514,
"facility": 13,
"format": 0
}
}
],
"result": 0
}
### [Add a Syslog destination](/docs/mdss/knowledge-base/siem-integration#add-a-syslog-destination)

Despite the path, `POST /api/externallogger/udpSyslog` creates **all three** Syslog variants — the `loggerType` field selects which.

{
"isEnabled": true,
"serverAddress": "siem.example.com",
"port": 6514,
"loggerType": 3,
"facility": 13,
"format": 0
}

| Field | Notes |
| --- | --- |
| `serverAddress` | Hostname or IP address. |
| `port` | Destination port. |
| `loggerType` | `0` UDP, `2` TCP, `3` TCP with TLS. |
| `facility` | `0`–`23`. Defaults to `1`. |
| `format` | `0` for RFC 5424. |

`PUT /api/externallogger/udpSyslog` takes the same body plus the `id` of the destination to update. All fields are replaced.

### [Add a Kafka destination](/docs/mdss/knowledge-base/siem-integration#add-a-kafka-destination)

`configuration` is a JSON **string** — serialise the security settings and pass them as an escaped string value, not as a nested object.

{
"isEnabled": true,
"serverAddressWithPortList": "broker1:9092,broker2:9092",
"loggerType": 1,
"topic": "mdss-audit",
"configuration": "{\"securityProtocol\":\"SASL_SSL\",\"saslMechanism\":\"SCRAM-SHA-512\",\"saslUsername\":\"mdss\",\"saslPassword\":\"...\"}"
}

The `configuration` string, unescaped:

{
"securityProtocol": "SASL_SSL",
"saslMechanism": "SCRAM-SHA-512",
"saslUsername": "mdss",
"saslPassword": "..."
}

`securityProtocol` accepts `PLAINTEXT`, `SSL`, `SASL_PLAINTEXT` or `SASL_SSL`. `saslMechanism` accepts `PLAIN`, `SCRAM-SHA-256` or `SCRAM-SHA-512`, and is only required for a SASL protocol.

`PUT /api/externallogger/kafka` takes the same body plus the `id`.

### [Enable, disable, and delete](/docs/mdss/knowledge-base/siem-integration#enable-disable-and-delete)

`PUT /api/externallogger/status` starts or stops delivery without changing the stored connection settings.

{
"id": "c9f1e0a4-...",
"isEnabled": false
}

`DELETE /api/externallogger/{id}` removes the configuration permanently. Delivery stops with the next event.

Responses carry a numeric `result` field and, on failure, a message. See [section 14](/docs/mdss/knowledge-base/siem-integration#14-troubleshooting) for the failure cases.

---

## [7. Message formats](/docs/mdss/knowledge-base/siem-integration#7-message-formats)

Both examples below are the same event — a file blocked as infected on an SMB share — as each transport delivers it.

### [Syslog, RFC 5424](/docs/mdss/knowledge-base/siem-integration#syslog-rfc-5424)

A standard RFC 5424 message. Every field appears twice: once inside the structured-data element `[meta ...]` as quoted key–value pairs, and once inside the human-readable message text. Parse the structured data; treat the message text as a description for analysts.

<14>1 2026-08-13T10:15:42.000000+00:00 mdss-host MetaDefenderStorageSecurity 7208 - [meta
fileName="invoice.docx"
filePath="/finance/2026/invoice.docx"
fileHash="5d41402abc4b2a76b9719d911017c592"
sha256="e3b0c44298fc1c149afbf4c8996fb924..."
fileSize="48213"
fileId="0199c0de-7a1e-7000-8000-0000000000ab"
dataId="bzIxMDgwOU5xTFZ2b2E"
result="Blocked"
blockedReason="Infected"
numberOfInfectedEngines="3"
AVCount="32"
threatFound="Ahnlab: Trojan/Win32.Agent"
storageName="Finance-SMB"
storageType="Category: FileShare, Protocol: Smb, Vendor: Generic"
storageId="stor-77"
scanId="scan-12"
scanName="Nightly Finance"
scanType="Scheduled Process"
Workflow="Default workflow"
LogType="1"
Category="0"
EventTimestamp="2026-08-13 10:15:42"
UserId="system"
UserName="system"
TenantId="default"
Namespace="ExternalLogger"
Id="0199c0de-7a1e-7000-8000-000000000001"]
File (fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; ... result:
"Blocked"; blockedReason: "Infected"; ...) from storage (name: "Finance-SMB"; ...)
was successfully scanned by scan (ID: "scan-12", ...) with the following
configuration "Default workflow".

Wrapped here for readability; on the wire each event is a single message.

> **Numeric values in Syslog**
>
> In RFC 5424 structured data all values are quoted strings, including numeric ones. Cast `fileSize`, `AVCount` and `numberOfInfectedEngines` in your parser if you need them as numbers.

### [Kafka, JSON](/docs/mdss/knowledge-base/siem-integration#kafka-json)

One JSON object per event, UTF-8 encoded. `Properties` holds the fields; the two message forms are provided alongside them so an event can be displayed without re-rendering it.

{
"Timestamp": "2026-08-13T10:15:42.0000000+00:00",
"Level": "Information",
"MessageTemplate": "File (fileName: {fileName}; filePath: {filePath}; ...",
"RenderedMessage": "File (fileName: \"invoice.docx\"; ...",
"Properties": {
"fileName": "invoice.docx",
"filePath": "/finance/2026/invoice.docx",
"fileHash": "5d41402abc4b2a76b9719d911017c592",
"sha256": "e3b0c44298fc1c149afbf4c8996fb924...",
"fileSize": 48213,
"fileId": "0199c0de-7a1e-7000-8000-0000000000ab",
"dataId": "bzIxMDgwOU5xTFZ2b2E",
"result": "Blocked",
"blockedReason": "Infected",
"numberOfInfectedEngines": 3,
"AVCount": 32,
"threatFound": "Ahnlab: Trojan/Win32.Agent",
"storageName": "Finance-SMB",
"storageType": "Category: FileShare, Protocol: Smb, Vendor: Generic",
"storageId": "stor-77",
"scanId": "scan-12",
"scanName": "Nightly Finance",
"scanType": "Scheduled Process",
"Workflow": "Default workflow",
"LogType": 1,
"Category": 0,
"EventTimestamp": "2026-08-13 10:15:42",
"UserId": "system",
"UserName": "system",
"TenantId": "default",
"Namespace": "ExternalLogger",
"Id": "0199c0de-7a1e-7000-8000-000000000001"
}
}

---

## [8. Event envelope reference](/docs/mdss/knowledge-base/siem-integration#8-event-envelope-reference)

These fields are present on **every** event, whatever its type. Build correlation rules and index-time extractions on these; everything else varies by event type.

| Field | Type | Description |
| --- | --- | --- |
| `Id` | string | Unique event identifier, a time-ordered UUID. Sorting by it sorts by creation order. Use it to deduplicate. |
| `Level` | string | `Information`, `Warning` or `Error`. `Error` marks a failed operation. |
| `LogType` | integer | The event type. See [section 10](/docs/mdss/knowledge-base/siem-integration#10-event-type-reference) for all values. |
| `Category` | integer | The functional group the event belongs to. Convenient for coarse filtering. |
| `Timestamp` | datetime | When the event was written, with offset. In Syslog this is the message header timestamp. |
| `EventTimestamp` | string | When the event occurred at its source. UTC, formatted `yyyy-MM-dd HH:mm:ss`. Prefer this for event time. |
| `UserId` | string | Identifier of the user who performed the action, or `system` for actions MDSS took on its own. |
| `UserName` | string | Display name of that user, or `system`. |
| `TenantId` | string | The tenant the event belongs to. Several tenants can share one collector and remain separable. |
| `Namespace` | string | Always `ExternalLogger`. A quick discriminator if the same collector receives other MDSS output. |
| `MessageTemplate` | string | Kafka only. The message text with field placeholders — a stable signature for an event type, unaffected by values. |
| `RenderedMessage` | string | Kafka only. The message with values substituted. In Syslog this is the message body. |

---

## [9. Scan event field reference](/docs/mdss/knowledge-base/siem-integration#9-scan-event-field-reference)

File-level events — discovery, scan and post actions — carry these fields in addition to the envelope. Which of them appear depends on how far the file has progressed, so **treat all non-envelope fields as optional** in your parser.

### [File identity — always present on file events](/docs/mdss/knowledge-base/siem-integration#file-identity--always-present-on-file-events)

| Field | Type | Description |
| --- | --- | --- |
| `fileName` | string | File name without path. |
| `filePath` | string | Full path within the storage unit. |
| `fileHash` | string | MDSS content hash for the file. |
| `fileSize` | integer | Size in bytes. |
| `fileId` | string | MDSS identifier for the file. Absent for files MDSS has not yet registered. |
| `lastModified` | datetime | Last-modified time reported by the storage. Present on discovery events. |

### [Scan result — present once the file has been scanned](/docs/mdss/knowledge-base/siem-integration#scan-result--present-once-the-file-has-been-scanned)

| Field | Type | Description |
| --- | --- | --- |
| `result` | string | The verdict, for example `Allowed` or `Blocked`. |
| `sha256` | string | SHA-256 of the file content, as computed by the scanning engine. |
| `dataId` | string | Scan identifier from MetaDefender. Use it to look up the full scan report, including per-engine detail. |
| `AVCount` | integer | How many anti-malware engines processed the file. |

### [Detection detail — present only when the verdict is blocked](/docs/mdss/knowledge-base/siem-integration#detection-detail--present-only-when-the-verdict-is-blocked)

| Field | Type | Description |
| --- | --- | --- |
| `blockedReason` | string | Why the file was blocked — an infection, a vulnerability, or sensitive data, according to the workflow's blocking rules. |
| `numberOfInfectedEngines` | integer | How many engines flagged the file. |
| `threatFound` | string | An engine name and the threat it reported, as a single string. |

### [Context — storage, scan, workflow and destination](/docs/mdss/knowledge-base/siem-integration#context--storage-scan-workflow-and-destination)

| Field | Type | Description |
| --- | --- | --- |
| `storageName` | string | Name of the storage unit the file was found in. |
| `storageType` | string | Category, protocol and vendor of that storage, as one descriptive string. |
| `storageId` | string | Identifier of the storage unit. |
| `scanId` | string | Identifier of the scan that processed the file. |
| `scanName` | string | Name of that scan. |
| `scanType` | string | `Real Time Process`, `Scheduled Process` or `Instant Process`. |
| `Workflow` | string | Name of the workflow applied. Present on successful scan events. |
| `PostAction` | string | Post-action events only. Which action was applied. |
| `destinationStorageName` | string | Move and copy actions only. Name of the destination storage. `destinationStorageType` and `destinationStorageId` accompany it. |
| `RelativeObjectName` | string | Move and copy actions only. Path the file was written to at the destination. |

### [File versions](/docs/mdss/knowledge-base/siem-integration#file-versions)

For storages that keep file versions, version-level events use parallel field names — `fileVersionName`, `fileVersionPath`, `fileVersionHash`, `fileVersionSize`, `fileVersionId` and `createdAt` — alongside `fileId` identifying the parent file.

---

## [10. Event type reference](/docs/mdss/knowledge-base/siem-integration#10-event-type-reference)

The full catalogue, grouped by category. `LogType` identifies the event. These numeric values are stable across releases — build filters and detection rules on them rather than on message text.

### [Category 0 — Scan activities](/docs/mdss/knowledge-base/siem-integration#category-0--scan-activities)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `0` | File discovered | A file was found in storage and registered. |
| `1` | File scanned | Carries the verdict. `Level` is `Error` when the file could not be scanned. |
| `2` | File discovery failed | Includes the failure reason. |
| `3` | File cancelled | Processing cancelled by a user. |
| `100`–`103` | Process started, completed, cancelled, failed | Scan-level lifecycle, one per scan run and storage. |
| `1500`–`1503` | Scan added, updated, deleted, imported | Scan configuration changes. |
| `1900`–`1904` | Schedule added, updated, deleted, imported, skipped | Scan schedule changes and skipped runs. |

### [Category 1 — Post actions](/docs/mdss/knowledge-base/siem-integration#category-1--post-actions)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `200` | File tagged | Tag written to the file or its metadata. |
| `205`–`206` | Blocked file moved, deleted | Includes the destination for moves. |
| `207` | Sanitized file moved | Deep CDR output written to the destination. |
| `208` | Allowed file moved |  |
| `209`–`211` | Blocked, sanitized, allowed file copied |  |
| `212`–`214` | Blocked, allowed, sanitized file kept | The file was left in place by policy. |
| `215` | Allowed file deleted |  |
| `216` | File versions scanned |  |
| `217`–`220` | Discovered file deleted, moved, copied, kept | Actions applied without scanning, from a discovery-only workflow. |
| `221` | Sanitized file deleted |  |
| `419` | Empty folders deleted | Lists the folder paths removed. |

### [Category 2 — Storage units](/docs/mdss/knowledge-base/siem-integration#category-2--storage-units)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `300`–`302` | Storage added, updated, removed |  |
| `400` | Real-time processing changed | Real-time protection enabled, disabled or reconfigured on a storage. |

### [Category 3 — Authentication](/docs/mdss/knowledge-base/siem-integration#category-3--authentication)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `600` | Signed in | Successful sign-ins only. See [section 12](/docs/mdss/knowledge-base/siem-integration#12-not-included-in-the-stream). |
| `601` | Signed out |  |

### [Category 4 — Settings](/docs/mdss/knowledge-base/siem-integration#category-4--settings)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `700`–`703` | Scan engine instance added, updated, deleted, imported |  |
| `750`–`753` | Scan pool added, updated, deleted, imported |  |
| `800`–`802` | Licence activated online, activated offline, deactivated |  |
| `900`–`901` | Configuration imported, exported |  |
| `950` | Notification settings changed | Also used for delivery results, under category 8. |
| `975` | SMTP configuration changed |  |
| `1000`–`1002` | External logger added, updated, deleted | Changes to this integration are themselves audited. |
| `1100` | Data retention changed | Retention enabled, disabled, or the window changed. |
| `1200`–`1202` | API key created, updated, deleted | Key lifecycle. Individual API calls are not audited. |
| `1300` | SSO configuration changed |  |
| `1410` | Workflow technologies changed | Which scanning technologies a workflow uses. |
| `1600` | On-demand scan requested | A user asked for a file or a filtered set to be scanned. |
| `2000` | Encryption key event | Key generation started, completed or failed. |
| `2200` | TLS certificate changed |  |
| `2300` | Telemetry configuration changed |  |

### [Category 6 — Users](/docs/mdss/knowledge-base/siem-integration#category-6--users)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `602`–`606` | User created, registered, role updated, updated, removed | Includes password resets and the property that changed. |
| `1800` | Product tour finalised |  |

### [Category 8 — Notifications](/docs/mdss/knowledge-base/siem-integration#category-8--notifications)

| `LogType` | Event | Notes |
| --- | --- | --- |
| `950` | Notification sent | Delivery result for an email, webhook or message-queue notification. |
| `1700` | Report generated |  |

### [Categories 9 to 13](/docs/mdss/knowledge-base/siem-integration#categories-9-to-13)

| Category | `LogType` | Event |
| --- | --- | --- |
| `9` Group units | `320`–`322` | Group added, updated, removed |
| `10` Account units | `330`–`332` | Account added, updated, removed |
| `11` Remediations | `2101`–`2103` | Remediation rule added, updated, deleted. Rule execution appears under category 1. |
| `12` Workflows | `1400`–`1404` | Workflow added, updated, deleted, set as default, imported |
| `13` Access control | `2400`–`2403` | Role assigned, removed, created, deleted |
| `13` Access control | `2410`–`2412` | Permission assigned, removed, roles replaced |

> **Reserved values**
>
> The schema defines 112 event types, of which 98 are in use. Event types `201`, `203`, `204`, `350`, `351` and `410`–`418`, and category `7`, are reserved and are not currently emitted. Category `5` is not defined. Do not build rules that depend on them, and handle unrecognised values without failing — new types may be added in later releases.

---

## [11. Filtering at the collector](/docs/mdss/knowledge-base/siem-integration#11-filtering-at-the-collector)

MDSS sends the whole audit stream to each enabled destination. There is no server-side filter by event type or severity.

On a large deployment, file-level events dominate the volume: a scan of one million files produces roughly one million discovery events plus one million scan events. If your SIEM licence is volume-based, filter before indexing.

`LogType` and `Category` are on every event and are designed for exactly this.

### [Security events only](/docs/mdss/knowledge-base/siem-integration#security-events-only)

Keep blocked files and the actions taken on them, plus all administrative activity. Drop routine discovery and per-file allow verdicts.

keep Category = 1 # all post actions
keep Category in (2,3,4,6,9,10,11,12,13) # all administrative activity
keep LogType = 1 and result = "Blocked" # blocked verdicts
keep Level = "Error" # every failure
drop everything else # discovery and allowed verdicts
### [Compliance and change-audit only](/docs/mdss/knowledge-base/siem-integration#compliance-and-change-audit-only)

Drop file-level events entirely and keep the administrative trail — a small, steady volume.

drop Category in (0,1)
keep everything else
### [Where to apply it](/docs/mdss/knowledge-base/siem-integration#where-to-apply-it)

| Transport | Approach |
| --- | --- |
| Kafka | Filter in your consumer or stream processor on `Properties.LogType` and `Properties.Category`. Cleanest option — unwanted events are never indexed and never counted. |
| Syslog | Filter on the relay, matching the structured-data pairs as substrings, for example `LogType="1"`. Both rsyslog and syslog-ng can do this with a message-content filter before forwarding. |
| SIEM ingest pipeline | Most platforms can drop events at ingest time. Confirm with your vendor whether dropped events still count toward your licence — often they do not. |

> **Size this before you enable it**
>
> Estimate volume from your file count and scan frequency, and agree the filter with whoever owns the SIEM licence. Turning on an unfiltered feed against a multi-million-file environment is the most common cause of an unpleasant surprise in the first week.

---

## [12. Not included in the stream](/docs/mdss/knowledge-base/siem-integration#12-not-included-in-the-stream)

External loggers carry the audit trail, and only the audit trail. The following are outside its scope in MDSS 4.5, listed so you can plan around them rather than discover them during integration.

| Not in the stream | What this means | Alternative |
| --- | --- | --- |
| Failed sign-in attempts | Successful sign-ins and sign-outs are emitted; failed attempts are not. The feed cannot be used for brute-force or password-spray detection against the MDSS console. | When MDSS is integrated with an identity provider through SSO, authentication failures appear in that provider's own logs. |
| Source address and session identifiers | Events identify the acting user by id and display name. There is no client IP address, host name, user agent or session identifier on any audit event, so events cannot be correlated by network location. | Access logs from the reverse proxy or load balancer in front of MDSS, shipped separately and joined on user and time. |
| Per-engine scan detail | A blocked file reports the number of engines that flagged it, the number that ran, and one engine-and-threat string. The full per-engine verdict list, CVE identifiers from vulnerability assessment, sensitive-data match detail, and the Deep CDR breakdown of what was removed are not on the wire. | `dataId` is present on every scanned-file event. Use it to retrieve the complete report from MDSS or MetaDefender Core. |
| API request activity | Audit events record outcomes, not requests. Individual REST calls, per-request API-key usage, and rejected calls such as permission denials are not audit events. Creating and deleting an API key is audited; using one is not. | Reverse proxy or gateway access logs. |
| Service and diagnostic logs | Application logs, stack traces, storage-adapter connection diagnostics, and everything in a support package stay local to the deployment. A failed scan appears as an audit event at `Error` level, without the underlying exception. | Collect the MDSS service log files with your existing log agent if you also want platform health in the SIEM. |
| Server-side event filtering | A destination is either enabled or disabled. There is no option to send only one category, only blocked files, or only a minimum severity to a given destination. | Filter at the collector — see [section 11](/docs/mdss/knowledge-base/siem-integration#11-filtering-at-the-collector). |
| Guaranteed delivery and replay | Delivery is best-effort. Events produced while a destination is unreachable are not re-sent when it recovers, so a collector outage becomes a gap in the SIEM's copy. The events themselves are never lost from MDSS. | Prefer TCP or TCP with TLS over UDP. Reconcile a known outage window with the audit API ([section 15](/docs/mdss/knowledge-base/siem-integration#15-pulling-audit-events-instead)). A highly available Kafka cluster is the most durable option. |
| CEF, LEEF and HTTP collectors | Syslog output is RFC 5424 with fields in the structured-data element. There is no CEF or LEEF formatter, and no HTTP event-collector transport for the audit stream. | Map the RFC 5424 structured data or the Kafka JSON to your platform's schema once during onboarding. Both provide named fields, so no pattern matching is required. |

---

## [13. Limits and tuning](/docs/mdss/knowledge-base/siem-integration#13-limits-and-tuning)

| Item | Value | Notes |
| --- | --- | --- |
| Destinations per type, per tenant | `5` | Counted separately for each of the four types. Exceeding it returns a specific error. |
| Syslog batch size | `100` | Events per batch. Set `SERILOG_BATCH_POSTING_LIMIT` to change it. |
| Kafka batch size | `50` | Events per batch. Set `KAFKA_BATCH_POSTING_LIMIT`. |
| Kafka batch interval | `5 s` | A partial batch is flushed after this interval. Set `KAFKA_BATCH_POSTING_PERIOD`. |
| Kafka delivery flush timeout | `10 s` | Per batch. |
| TLS certificate validation | enabled | For Syslog TCP with TLS. `EXTERNAL_LOGGER_TCP_TLS_IGNORE_CERTIFICATES` can relax it to ignore chain errors, or all errors, for a collector with a self-signed certificate. |
| Retention of delivered events | not applicable | The MDSS data-retention policy trims the MDSS audit database only. Events already delivered are unaffected, so retention in the SIEM is governed entirely by the SIEM. |

> **On relaxing TLS validation**
>
> Only do this for a collector whose certificate you control and cannot get signed. It is a deployment-wide setting and applies to every Syslog TLS destination.

---

## [14. Troubleshooting](/docs/mdss/knowledge-base/siem-integration#14-troubleshooting)

### [The configuration will not save](/docs/mdss/knowledge-base/siem-integration#the-configuration-will-not-save)

MDSS validates a destination before storing it. The failure cases are:

| Result | Cause | Resolution |
| --- | --- | --- |
| Failed to test configuration | The connection test did not succeed — wrong address or port, the collector is not listening, a firewall is blocking the path, or TLS validation failed. | Verify reachability from the MDSS host, then retry. For TLS, confirm the collector's certificate chain is trusted. |
| Same configuration | An identical destination already exists. | Edit the existing entry instead of adding a second one. |
| Number of integrations exceeded | Five destinations of this type already exist. | Delete one, or use a relay to fan out beyond five. |
| Already enabled / already disabled | The status change requested is the current state. | No action needed. |
| Not found | The `id` does not exist for this tenant. | List the destinations and use a current id. |

### [The destination saved, but no events arrive](/docs/mdss/knowledge-base/siem-integration#the-destination-saved-but-no-events-arrive)

- Check the destination is **enabled**. A saved configuration with delivery switched off is silent.
- Confirm MDSS is producing audit events at all — open the console audit log. If it is empty, no destination will receive anything. Run a small scan to generate events.
- For UDP, remember there is no delivery confirmation. A firewall can drop the traffic silently and both ends will look healthy. Retest with TCP to prove the path.
- For Kafka, verify the topic exists and that the credentials have produce rights on it.
- If a collector-side filter is in place, confirm it is not dropping everything. Match on `Namespace="ExternalLogger"` first to prove events are arriving, then narrow.

### [Events arrive but fields are missing](/docs/mdss/knowledge-base/siem-integration#events-arrive-but-fields-are-missing)

Field composition varies by event type and by how far a file has progressed — a discovered file carries no verdict, and an allowed file carries no `blockedReason`. This is expected. See [section 9](/docs/mdss/knowledge-base/siem-integration#9-scan-event-field-reference) for which fields appear when, and treat all non-envelope fields as optional.

### [Timestamps look wrong](/docs/mdss/knowledge-base/siem-integration#timestamps-look-wrong)

`EventTimestamp` is always UTC. `Timestamp` carries an explicit offset. If events appear shifted, check the time zone your SIEM applies at ingest rather than the MDSS configuration.

---

## [15. Pulling audit events instead](/docs/mdss/knowledge-base/siem-integration#15-pulling-audit-events-instead)

Where a push feed is not wanted, or to reconcile a period when a destination was unreachable, the same audit events are available on the REST API.

GET /api/audit/{startIndex}/{count}

Returns audit entries with filtering, and a total count. The total is capped at 10,001 as a performance guard, so narrow the filter rather than paging through an unbounded result set.

The MDSS data-retention policy applies to this API — events older than the configured retention window are no longer available. For long-term retention, the SIEM copy is the record.

---

## [16. Questions that come up](/docs/mdss/knowledge-base/siem-integration#16-questions-that-come-up)

**"Is SIEM integration an extra licence?"** No. External loggers are part of the product.

**"Which SIEMs are supported?"** Any platform that can receive RFC 5424 Syslog or consume from a Kafka topic. There is no per-vendor integration to install; the fields are named in both formats, so mapping to a platform's schema is a one-time configuration task.

**"Can we send different events to different destinations?"** Not from MDSS. Every enabled destination receives the whole stream. Route and filter at the collector.

**"Can we send to more than five collectors?"** Five per type is the limit — twenty in total across the four types. Beyond that, send to a relay and fan out from there.

**"Will this slow down our scans?"** No. The audit database write is independent of the external destinations, and a slow or unreachable collector does not delay scanning.

**"What happens if our SIEM goes down?"** Delivery is best-effort and not replayed, so those events will be missing from the SIEM's copy. They remain in the MDSS audit database and can be recovered with the audit API within the retention window.

**"Is the traffic encrypted?"** Use Syslog over TCP with TLS, or Kafka with `SSL` or `SASL_SSL`. Plain UDP and TCP Syslog are unencrypted.

**"Do we get the full scan report for every file?"** You get the verdict, the reason, engine counts, a named threat, and both hashes. For the full per-engine report, pivot into MDSS or MetaDefender Core on the `dataId` carried in the event.

**"Can we get failed login alerts from MDSS?"** Not from this feed in 4.5 — only successful sign-ins and sign-outs are emitted. Where MDSS uses SSO, the identity provider's logs carry authentication failures.

---

## [17. Where to go deeper](/docs/mdss/knowledge-base/siem-integration#17-where-to-go-deeper)

| Topic | Where to look |
| --- | --- |
| Full API endpoint reference | [MetaDefender Storage Security API](/docs/mdss/metadefender-storage-security-api) |
| Audit log in the console | **Audit log** in the MDSS navigation |
| Configuring destinations | **Settings → External loggers** |
| Data retention settings | **Settings → Data retention** |
| Notification webhooks and message-queue notifications | [File scanned RabbitMQ notifications](/docs/mdss/configuration/file-scanned-rabbitmq-notifications) |
| Environment variables and deployment tuning | Deployment documentation |
| Sizing the feed for a large environment | Sales Engineering |
