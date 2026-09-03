<!-- source: https://www.opswat.com/docs/mdss/configuration/syslog-message-reference -->

# Syslog Message Reference — One Sample per Event Type

This page lists a sample Syslog message for every event type MDSS can emit to an external logger. Use it to build parsers, field extractions and detection rules without having to generate each event first.

MDSS emits 98 distinct event types across 12 categories. Each is listed below with its `LogType` value, the fields it carries, and a complete sample message.

For how to configure a Syslog destination, see **External Loggers — Streaming the MDSS Audit Trail to a SIEM**.

---

## [1. Message anatomy](/docs/mdss/configuration/syslog-message-reference#1-message-anatomy)

Every message is a standard RFC 5424 line with five parts:

<110>1 2026-08-13T12:15:42.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta ...] Message text
└─┬─┘│ └───────────────┬──────────────┘ └─────┬────┘ └───────────┬──────────┘ └─┬─┘ │ └───┬──┘ └────┬─────┘
│ │ │ │ │ │ │ │ │
PRI │ timestamp hostname app-name proc-id │ structured message
version msg-id data

| Part | Notes |
| --- | --- |
| PRI | `facility × 8 + severity`. With the default `LogAudit` facility (13): `110` for informational, `108` for warning, `107` for error. Change the facility in the destination configuration and every PRI shifts accordingly. |
| Timestamp | Local time of the MDSS host, with UTC offset. |
| Hostname | The MDSS host that emitted the event. |
| App-name | Always `MetaDefenderStorageSecurity`. |
| Proc-id | Process id of the MDSS logging service. Not stable across restarts. |
| Msg-id | Always `-` (not used). |
| Structured data | A single `[meta ...]` element containing every field as a quoted key–value pair. |
| Message | Human-readable text. Field values are substituted inline. |

### [What is inside `[meta ...]`](/docs/mdss/configuration/syslog-message-reference#what-is-inside-meta-)

Two groups of fields, in one element:

1. **Message fields** — one pair for every placeholder in the message text. These vary by event type and are listed per event below.
2. **Envelope fields** — present on every event: `TenantId`, `UserName`, `UserId`, `EventTimestamp`, `Category`, `LogType`, `Namespace`, `Id`.

> **Key on names, not position**
>
> Field order inside `[meta ...]` is not part of the contract and may change between releases. Always parse by key name. Likewise, treat message fields as optional — the same event type carries different fields depending on what MDSS knows at the time.

### [Two conventions to note](/docs/mdss/configuration/syslog-message-reference#two-conventions-to-note)

**All values are quoted strings.** RFC 5424 structured data has no types, so `fileSize="48213"` is a string even though it is a number. Cast in your parser.

**String values are quoted in the message text too.** The message reads `... fileName: "invoice.docx" ...`, with the quotes present. Numeric values appear unquoted. This affects regular expressions written against the message body — prefer the structured data.

### [A complete example](/docs/mdss/configuration/syslog-message-reference#a-complete-example)

The most detailed event in the product, with nothing elided — a blocked file, `LogType` `1`:

<110>1 2026-08-13T12:15:42.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" dataId="bzIxMDgwOU5xTFZ2b2E" sha256="e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855" result="Blocked" blockedReason="Infected" numberOfInfectedEngines="3" AVCount="32" threatFound="Ahnlab: Trojan/Win32.Agent" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" Workflow="Default workflow" TenantId="default" UserName="system" UserId="system" EventTimestamp="2026-08-13 10:15:42" Category="0" LogType="1" Namespace="ExternalLogger" Id="0199c0de-7a1e-7000-8000-000000000001"] File (fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; fileHash: "5d41402abc4b2a76b9719d911017c592"; fileSize: 48213; fileId: "0199c0de-7a1e-7000-8000-0000000000ab"; dataId: "bzIxMDgwOU5xTFZ2b2E"; sha256:"e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"; result: "Blocked"; blockedReason: "Infected"; numberOfInfectedEngines: 3; AVCount: 32; threatFound:"Ahnlab: Trojan/Win32.Agent") from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") was successfully scanned by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process") with the following configuration "Default workflow".

**For readability, the samples in sections 3 to 14 show the message text and the message fields, with the eight envelope fields abbreviated to <envelope>.** Substitute the envelope from the example above; only `Category`, `LogType`, `UserName` and `UserId` change between event types, and those are stated in each entry.

### [Sample environment](/docs/mdss/configuration/syslog-message-reference#sample-environment)

All samples use one consistent fictional deployment:

| Item | Value |
| --- | --- |
| Host | `mdss-prod-01` |
| Administrator | `John Davis (jdavis)`, id `e69e8c2d-4dcc-4489-8f40-0df84199de52` |
| Storage | `Finance-SMB`, id `7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73`, SMB file share |
| Scan | `Nightly Finance`, id `e1b6d842-0f37-4c9b-8a15-63d0947fe2ba`, scheduled |
| Workflow | `Default workflow`, id `9d4e1f60-3a72-4b85-8c19-f2073be5a1c8` |
| File | `invoice.docx` at `/finance/2026/invoice.docx` |
| Tenant | `default` |

---

## [2. Reading the actor fields](/docs/mdss/configuration/syslog-message-reference#2-reading-the-actor-fields)

`UserName` and `UserId` identify who caused the event.

- For an administrator action, both carry that account's values — `UserName="jdavis"`.
- For anything MDSS does on its own — discovery, scanning, remediation, notification delivery — both carry the literal string `system`.

This is the fastest way to separate operator activity from automated processing: filter on `UserName="system"`.

---

## [3. Category 0 — Scan activities](/docs/mdss/configuration/syslog-message-reference#3-category-0--scan-activities)

`Category="0"`. File discovery and scanning, scan process lifecycle, and scan and schedule configuration changes.

### [LogType 0 — File discovered](/docs/mdss/configuration/syslog-message-reference#logtype-0--file-discovered)

A file was found in storage and registered. `UserName="system"`.

Message fields: `fileName`, `filePath`, `fileHash`, `fileSize`, `fileId`, `lastModified`, `storageName`, `storageType`, `storageId`, `scanId`, `scanName`, `scanType`.

<110>1 2026-08-13T12:15:42.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="0" LogType="0" UserName="system">] File(fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; fileHash: "5d41402abc4b2a76b9719d911017c592"; fileSize: 48213; fileId: "0199c0de-7a1e-7000-8000-0000000000ab"; lastModified: 08/12/2026 16:40:11) from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") was discovered by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process")

**Real-time variant.** When the scan is real-time, the message gains a discovery mode and a `HandlingType` field:

... was discovered by scan (ID: "5a20c7e9-8b41-4f63-9d28-1e7c05ab3f94", name: "Real Time Process", type: "Real Time Process") (Discovery mode: "EventBased")
### [LogType 1 — File scanned](/docs/mdss/configuration/syslog-message-reference#logtype-1--file-scanned)

The verdict for a file. `UserName="system"`. See the complete example in section 1.

Field composition depends on the outcome:

| Outcome | Message fields |
| --- | --- |
| Allowed | `fileName`, `filePath`, `fileHash`, `sha256`, `fileSize`, `fileId`, `dataId`, `result`, `AVCount`, plus storage, scan and `Workflow` |
| Blocked | The above plus `blockedReason`, `numberOfInfectedEngines`, `threatFound` |
| Not yet scanned | Identity only — `fileName`, `filePath`, `fileHash`, `fileSize`, `fileId`, `lastModified` |

**Allowed file:**

<110>1 2026-08-13T12:15:44.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta fileName="policy.pdf" filePath="/finance/2026/policy.pdf" fileHash="8b1a9953c4611296a827abf8c47804d7" sha256="9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08" fileSize="120344" fileId="0199c0de-7a1e-7000-8000-0000000000ac" dataId="bzIxMDgwOVJrTXBXcWI" result="Allowed" AVCount="32" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" Workflow="Default workflow" <envelope Category="0" LogType="1" UserName="system">] File (fileName: "policy.pdf"; filePath: "/finance/2026/policy.pdf"; fileHash: "8b1a9953c4611296a827abf8c47804d7"; sha256:"9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08"; fileSize: 120344; fileId: "0199c0de-7a1e-7000-8000-0000000000ac"; dataId: "bzIxMDgwOVJrTXBXcWI"; result: "Allowed"; AVCount: 32 ) from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") was successfully scanned by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process") with the following configuration "Default workflow".

**Scan failure** — emitted at error severity, PRI `<107>`, with a different message and no verdict fields:

<107>1 2026-08-13T12:15:46.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta fileName="archive.zip" filePath="/finance/2026/archive.zip" fileHash="c4ca4238a0b923820dcc509a6f75849b" fileSize="9812443" fileId="0199c0de-7a1e-7000-8000-0000000000ad" lastModified="08/12/2026 09:02:55" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="0" LogType="1" UserName="system">] Unable to scan file (fileName: "archive.zip"; filePath: "/finance/2026/archive.zip"; fileHash: "c4ca4238a0b923820dcc509a6f75849b"; fileSize: 9812443; fileId: "0199c0de-7a1e-7000-8000-0000000000ad"; lastModified: 08/12/2026 09:02:55) from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process")

**Scanned with identity.** When MDSS reuses a previous result instead of rescanning, the text reads `was successfully scanned with identity` in place of `was successfully scanned`.

**File version variant.** On storages that keep versions, the label becomes `File version` and the fields are `fileVersionName`, `fileId`, `fileVersionPath`, `fileVersionHash`, `fileVersionSize`, `fileVersionId`, `createdAt`.

### [LogType 2 — File discovery failed](/docs/mdss/configuration/syslog-message-reference#logtype-2--file-discovery-failed)

Discovery could not complete for one file. Emitted at error severity, PRI `<107>`. `UserName="system"`.

Message fields: `ObjectId`, `objectPath`, storage, scan, `FailureReason`.

<107>1 2026-08-13T12:15:48.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta ObjectId="0199c0de-7a1e-7000-8000-0000000000ae" objectPath="/finance/2026/locked.xlsx" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" FailureReason="Access denied" <envelope Category="0" LogType="2" UserName="system">] Unable to discover file with ID "0199c0de-7a1e-7000-8000-0000000000ae" with path "/finance/2026/locked.xlsx" from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process"). Reason: "Access denied"
> **File skipped uses this same event type**
>
> When a file is skipped rather than failed — excluded by a filter, for example — MDSS emits `LogType="2"` at **warning** severity, PRI `<108>`, with the same message shape and the skip reason in `FailureReason`. Distinguish the two by severity, not by event type.

### [LogType 3 — File cancelled](/docs/mdss/configuration/syslog-message-reference#logtype-3--file-cancelled)

A user cancelled processing for a file. Carries that user's identity, not `system`.

Message fields: file identity fields.

<110>1 2026-08-13T12:16:02.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" <envelope Category="0" LogType="3" UserName="jdavis">] File (fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; fileHash: "5d41402abc4b2a76b9719d911017c592"; fileSize: 48213; fileId: "0199c0de-7a1e-7000-8000-0000000000ab"; lastModified: 08/12/2026 16:40:11) has been cancelled
### [LogType 100 to 103 — Scan process lifecycle](/docs/mdss/configuration/syslog-message-reference#logtype-100-to-103--scan-process-lifecycle)

One event per scan run and storage. `UserName="system"`. The `ScanType` field holds the lifecycle action, lower-cased.

| `LogType` | Action | Severity |
| --- | --- | --- |
| `100` | `started` | informational, `<110>` |
| `101` | `completed` | informational, `<110>` |
| `102` | `cancelled` | informational, `<110>` |
| `103` | `failed` | error, `<107>` |

<110>1 2026-08-13T12:15:40.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" ScanType="started" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" <envelope Category="0" LogType="100" UserName="system">] Scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process") "started" for storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73")

Substitute `ScanType="completed"` with `LogType="101"`, `ScanType="cancelled"` with `LogType="102"`, and `ScanType="failed"` with `LogType="103"` and PRI `<107>`.

> **Two fields named for the scan type**
>
> `scanType` (lower case s) is the kind of scan — `Scheduled Process`, `Real Time Process` or `Instant Process`. `ScanType` (upper case S) is the lifecycle action on these four event types. They are different fields.

### [LogType 1500 to 1503 — Scan configuration changed](/docs/mdss/configuration/syslog-message-reference#logtype-1500-to-1503--scan-configuration-changed)

An administrator added, updated, deleted or imported a scan.

| `LogType` | `Action` |
| --- | --- |
| `1500` | `added` |
| `1501` | `updated` |
| `1502` | `deleted` |
| `1503` | `imported` |

Message fields: `Scan`, `Type`, `Action`, `User`. Add and update also carry `WorkflowName`, `UserAgent`, `WorkflowRule`, `ScanPoolName`, `ScanInstances`. Add, update and delete also carry the storage fields.

<110>1 2026-08-13T09:22:10.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Scan="Nightly Finance" Type="Scheduled" Action="added" User="jdavis" WorkflowName="Default workflow" UserAgent="" WorkflowRule="" ScanPoolName="Primary pool" ScanInstances="https://core-01:8008" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" <envelope Category="0" LogType="1500" UserName="jdavis">] Scan "Nightly Finance", type: "Scheduled" was "added" by "jdavis". Workflow: name - "Default workflow", user agent - "", workflow rule - "". Scan pool: name - "Primary pool", scan instances - "https://core-01:8008". Storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73")

**Failure variant** — error severity, PRI `<107>`, fields `User`, `Action`, `Scan`, `ResponseMessage`:

<107>1 2026-08-13T09:22:12.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="jdavis" Action="add" Scan="Nightly Finance" ResponseMessage="A scan with this name already exists" <envelope Category="0" LogType="1500" UserName="jdavis">] User "jdavis" was unable to "add" scan "Nightly Finance". Response message: "A scan with this name already exists".
### [LogType 1900 to 1904 — Scan schedule changed](/docs/mdss/configuration/syslog-message-reference#logtype-1900-to-1904--scan-schedule-changed)

| `LogType` | `Action` |
| --- | --- |
| `1900` | `added` |
| `1901` | `updated` |
| `1902` | `deleted` |
| `1903` | `imported` |
| `1904` | `skipped` |

Message fields: `scanName`, `scanId`, `Action`, `User`, storage fields, `WorkflowId`, `WorkflowName`.

<110>1 2026-08-13T09:25:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta scanName="Nightly Finance" scanId="b83f27a5-14c9-4e06-9f7b-2d58e0ca934f" Action="added" User="jdavis" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" WorkflowName="Default workflow" <envelope Category="0" LogType="1900" UserName="jdavis">] Scan schedule (Name: "Nightly Finance"; ID: "b83f27a5-14c9-4e06-9f7b-2d58e0ca934f";) was "added" by "jdavis" for storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") with Workflow (Id: "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8"; Name: "Default workflow")

`LogType="1904"` uses `Action="skipped"` and is emitted by the system when a scheduled run is skipped, so `UserName="system"`.

**Failure variant** — error severity, PRI `<107>`:

<107>1 2026-08-13T09:25:04.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="jdavis" Action="add" scanName="Nightly Finance" scanId="b83f27a5-14c9-4e06-9f7b-2d58e0ca934f" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" <envelope Category="0" LogType="1900" UserName="jdavis">] User "jdavis" was unable to "add" scan schedule (Name: "Nightly Finance"; ID: "b83f27a5-14c9-4e06-9f7b-2d58e0ca934f";) (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73")

---

## [4. Category 1 — Post actions](/docs/mdss/configuration/syslog-message-reference#4-category-1--post-actions)

`Category="1"`. What MDSS did about each file after scanning. All are emitted by the system, so `UserName="system"`.

Every post-action event shares one message shape:

{PostAction} applied to file {file fields} from storage {storage fields} by scan {scan fields}. {outcome sentence}

`PostAction` holds one of: `Tagging`, `Blocked file remediation`, `Allowed file remediation`, `Discovered file remediation`, `Scan file versions`.

### [LogType 200 — File tagged](/docs/mdss/configuration/syslog-message-reference#logtype-200--file-tagged)

Message fields: `PostAction`, file identity, storage, scan.

<110>1 2026-08-13T12:15:50.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta PostAction="Tagging" fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="1" LogType="200" UserName="system">] "Tagging" applied to file (fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; fileHash: "5d41402abc4b2a76b9719d911017c592"; fileSize: 48213; fileId: "0199c0de-7a1e-7000-8000-0000000000ab"; lastModified: 08/12/2026 16:40:11) from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process").
### [LogType 205 — Blocked file moved](/docs/mdss/configuration/syslog-message-reference#logtype-205--blocked-file-moved)

Move and copy actions add three destination fields: `destinationStorageName`, `destinationStorageType`, `destinationStorageId`, and `RelativeObjectName` for the path written at the destination.

<110>1 2026-08-13T12:15:52.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta PostAction="Blocked file remediation" fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" destinationStorageName="Quarantine-SMB" destinationStorageType="Category: FileShare, Protocol: Smb, Vendor: Generic" destinationStorageId="2c94f0b7-6d13-4e8a-b5f2-90a7cd31e648" RelativeObjectName="/quarantine/2026-08-13/invoice.docx" <envelope Category="1" LogType="205" UserName="system">] "Blocked file remediation" applied to file (fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; fileHash: "5d41402abc4b2a76b9719d911017c592"; fileSize: 48213; fileId: "0199c0de-7a1e-7000-8000-0000000000ab"; lastModified: 08/12/2026 16:40:11) from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process"). The blocked file was moved to storage (name: "Quarantine-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "2c94f0b7-6d13-4e8a-b5f2-90a7cd31e648") Destination objectPath: "/quarantine/2026-08-13/invoice.docx"
### [LogType 206 — Blocked file deleted](/docs/mdss/configuration/syslog-message-reference#logtype-206--blocked-file-deleted)

No destination fields. Outcome sentence: `The blocked file was deleted.`

<110>1 2026-08-13T12:15:53.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta PostAction="Blocked file remediation" fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="1" LogType="206" UserName="system">] "Blocked file remediation" applied to file (fileName: "invoice.docx"; ...) from storage (name: "Finance-SMB"; ...) by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", ...). The blocked file was deleted.
### [LogType 207 to 215 — Remaining move, copy, delete and keep actions](/docs/mdss/configuration/syslog-message-reference#logtype-207-to-215--remaining-move-copy-delete-and-keep-actions)

All share the shape above. The differences are `PostAction`, `LogType`, and the outcome sentence.

| `LogType` | Event | `PostAction` | Outcome sentence | Destination fields |
| --- | --- | --- | --- | --- |
| `207` | Sanitized file moved | `Allowed file remediation` | `The sanitized file was moved to storage ...` | yes |
| `208` | Allowed file moved | `Allowed file remediation` | `The allowed file was moved to storage ...` | yes |
| `209` | Blocked file copied | `Blocked file remediation` | `The blocked file was copied to storage ...` | yes |
| `210` | Sanitized file copied | `Allowed file remediation` | `The sanitized file was copied to storage ...` | yes |
| `211` | Allowed file copied | `Allowed file remediation` | `The allowed file was copied to storage ...` | yes |
| `212` | Blocked file kept | `Blocked file remediation` | `The blocked file was kept.` | no |
| `213` | Allowed file kept | `Allowed file remediation` | `The allowed file was kept.` | no |
| `214` | Sanitized file kept | `Allowed file remediation` | `The sanitized file was kept on storage ...` | yes |
| `215` | Allowed file deleted | `Allowed file remediation` | `The allowed file was deleted from storage.` | no |
| `221` | Sanitized file deleted | `Allowed file remediation` | `The sanitized file was deleted from storage ...` | yes |

> **PostAction does not distinguish sanitised from allowed**
>
> Sanitised-file remediations report `PostAction="Allowed file remediation"`. Use `LogType` to identify the specific action, not the `PostAction` text.

### [LogType 216 — File versions scanned](/docs/mdss/configuration/syslog-message-reference#logtype-216--file-versions-scanned)

`PostAction="Scan file versions"`, no destination fields, no outcome sentence beyond the base text.

<110>1 2026-08-13T12:15:55.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta PostAction="Scan file versions" fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="1" LogType="216" UserName="system">] "Scan file versions" applied to file (fileName: "invoice.docx"; ...) from storage (name: "Finance-SMB"; ...) by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", ...).
### [LogType 217 to 220 — Discovered file actions](/docs/mdss/configuration/syslog-message-reference#logtype-217-to-220--discovered-file-actions)

Applied without scanning, by a discovery-only workflow. `PostAction="Discovered file remediation"`.

| `LogType` | Event | Outcome sentence | Destination fields |
| --- | --- | --- | --- |
| `217` | Discovered file deleted | `The discovered file was deleted from storage.` | no |
| `218` | Discovered file moved | `The discovered file was moved to storage ...` | yes |
| `219` | Discovered file copied | `The discovered file was copied to storage ...` | yes |
| `220` | Discovered file kept | `The discovered file was kept.` | no |

<110>1 2026-08-13T12:15:57.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta PostAction="Discovered file remediation" fileName="old-report.xls" filePath="/finance/archive/old-report.xls" fileHash="a87ff679a2f3e71d9181a67b7542122c" fileSize="22100" fileId="0199c0de-7a1e-7000-8000-0000000000af" lastModified="03/02/2024 11:20:00" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="1" LogType="217" UserName="system">] "Discovered file remediation" applied to file (fileName: "old-report.xls"; filePath: "/finance/archive/old-report.xls"; fileHash: "a87ff679a2f3e71d9181a67b7542122c"; fileSize: 22100; fileId: "0199c0de-7a1e-7000-8000-0000000000af"; lastModified: 03/02/2024 11:20:00) from storage (name: "Finance-SMB"; ...) by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", ...). The discovered file was deleted from storage.
### [Post-action failure](/docs/mdss/configuration/syslog-message-reference#post-action-failure)

Any post action that fails is emitted at error severity, PRI `<107>`, with the same `LogType` and a different message:

<107>1 2026-08-13T12:15:58.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta PostAction="Blocked file remediation" fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="1" LogType="205" UserName="system">] "Blocked file remediation" failed for file (fileName: "invoice.docx"; ...) from storage (name: "Finance-SMB"; ...) by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", ...)
### [LogType 419 — Empty folders deleted](/docs/mdss/configuration/syslog-message-reference#logtype-419--empty-folders-deleted)

Folder paths are embedded directly in the message text, not as a field.

<110>1 2026-08-13T12:16:10.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="1" LogType="419" UserName="system">] The following empty folders have been deleted: [/finance/2026/tmp, /finance/2026/old] from storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") by scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process") .

---

## [5. Category 2 — Storage units](/docs/mdss/configuration/syslog-message-reference#5-category-2--storage-units)

`Category="2"`.

### [LogType 300 to 302 — Storage added, updated, removed](/docs/mdss/configuration/syslog-message-reference#logtype-300-to-302--storage-added-updated-removed)

| `LogType` | `Action` |
| --- | --- |
| `300` | `added` |
| `301` | `updated` |
| `302` | `removed` |

Message fields: `storageName`, `storageType`, `storageId`, `Action`, `User`.

<110>1 2026-08-13T09:10:22.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" Action="added" User="jdavis" <envelope Category="2" LogType="300" UserName="jdavis">] Storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") was "added" by "jdavis".

**Failure variant** — error severity, PRI `<107>`. `was` becomes `could not be`:

... Storage (name: "Finance-SMB"; ...) could not be "added" by "jdavis".
### [LogType 400 — Real-time processing changed](/docs/mdss/configuration/syslog-message-reference#logtype-400--real-time-processing-changed)

Real-time protection enabled, disabled or reconfigured on a storage.

**Enabled**, with a backfill start date:

<110>1 2026-08-13T09:12:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="enabled" User="jdavis" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" RealTimeStartDate="2026-08-13T00:00:00.000Z" <envelope Category="2" LogType="400" UserName="jdavis">] Real Time Process was "enabled" by "jdavis" for storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73") discovering files modified since "2026-08-13T00:00:00.000Z"

**Disabled** — same shape with `Action="disabled"` and no `RealTimeStartDate`.

**Handling type changed** — a different message and a `NewHandlingType` field:

<110>1 2026-08-13T09:13:30.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta NewHandlingType="EventBased" User="jdavis" storageName="Finance-SMB" storageType="Category: FileShare, Protocol: Smb, Vendor: Generic" storageId="7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73" <envelope Category="2" LogType="400" UserName="jdavis">] Real Time Process handling type was changed to "EventBased" by "jdavis" for storage (name: "Finance-SMB"; "Category: FileShare, Protocol: Smb, Vendor: Generic"; ID: "7f3a9c14-2b8e-4d51-9a06-c1e5b48f2d73")

**Failure variant** — error severity, PRI `<107>`, `was` becomes `could not be`.

---

## [6. Category 3 — Authentication](/docs/mdss/configuration/syslog-message-reference#6-category-3--authentication)

`Category="3"`.

### [LogType 600 — Signed in](/docs/mdss/configuration/syslog-message-reference#logtype-600--signed-in)

Message field: `User`, the account's full name and user name.

<110>1 2026-08-13T12:15:42.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="John Davis (jdavis)" <envelope Category="3" LogType="600" UserName="jdavis">] "John Davis (jdavis)" logged in.
> **Failed sign-ins are not emitted**
>
> MDSS 4.5 emits this event only on a successful sign-in. There is no event for a rejected sign-in attempt, so this feed cannot be used for brute-force detection. Where MDSS runs behind SSO, the identity provider's own logs carry authentication failures.

### [LogType 601 — Signed out](/docs/mdss/configuration/syslog-message-reference#logtype-601--signed-out)

<110>1 2026-08-13T13:02:19.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="John Davis (jdavis)" <envelope Category="3" LogType="601" UserName="jdavis">] "John Davis (jdavis)" logged out.

A sign-out that does not complete cleanly is emitted at warning severity, PRI `<108>`, with the text `"John Davis (jdavis)" encountered an issue while logging out.`

---

## [7. Category 4 — Settings](/docs/mdss/configuration/syslog-message-reference#7-category-4--settings)

`Category="4"`. Configuration changes across the product.

### [LogType 700 to 703 — Scan engine instance changed](/docs/mdss/configuration/syslog-message-reference#logtype-700-to-703--scan-engine-instance-changed)

Message fields: `ScanInstance` (the engine URL), `Action`.

| `LogType` | `Action` |
| --- | --- |
| `700` | `added` |
| `701` | `updated` |
| `702` | `deleted` |
| `703` | `imported` |

<110>1 2026-08-13T08:40:05.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta ScanInstance="https://core-01:8008" Action="added" <envelope Category="4" LogType="700" UserName="jdavis">] Scan Instance "https://core-01:8008" was "added" by "jdavis".

**Failure variant** — error severity, PRI `<107>`, with `ResponseMessage`:

<107>1 ... [meta Action="add" ScanInstance="https://core-01:8008" ResponseMessage="Connection refused" <envelope Category="4" LogType="700" UserName="jdavis">] Unable to "add" Scan Instance "https://core-01:8008". Response message: "Connection refused".
### [LogType 750 to 753 — Scan pool changed](/docs/mdss/configuration/syslog-message-reference#logtype-750-to-753--scan-pool-changed)

Message fields: `ScanPool` (the pool name), `Action`. Same actions and failure shape as scan instances.

<110>1 2026-08-13T08:42:11.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta ScanPool="Primary pool" Action="added" <envelope Category="4" LogType="750" UserName="jdavis">] Scan Pool "Primary pool" was "added" by "jdavis".
### [LogType 800 to 802 — Licence activation](/docs/mdss/configuration/syslog-message-reference#logtype-800-to-802--licence-activation)

Message fields: `Action`, `User`.

| `LogType` | `Action` |
| --- | --- |
| `800` | `online activated` |
| `801` | `offline activated` |
| `802` | `deactivated` |

<110>1 2026-08-13T08:05:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="online activated " User="jdavis" <envelope Category="4" LogType="800" UserName="jdavis">] License was "online activated " by "jdavis".

**Failure variant** — error severity, PRI `<107>`. `was` becomes `failed to be`.

### [LogType 900 — Configuration imported](/docs/mdss/configuration/syslog-message-reference#logtype-900--configuration-imported)

Message fields: `Action`, `User`. The inclusion summary is part of the message text.

<110>1 2026-08-13T08:12:44.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="imported" User="jdavis" <envelope Category="4" LogType="900" UserName="jdavis">] Configuration was "imported" by "jdavis". License was included. SMTP configuration was included. Retention configuration was not included. Notifications configuration was partially included. Users were included

**Failure variant** — error severity, PRI `<107>`, with `FailureReason`:

<107>1 ... [meta Action="imported" User="jdavis" FailureReason="the provided password is incorrect" <envelope Category="4" LogType="900" UserName="jdavis">] Configuration failed to be "imported" by "jdavis" because "the provided password is incorrect".

Other failure reasons: `the configuration file could not be upgraded`, `the configuration file is empty`, `the license could not be activated`, `the deserialization of the configuration file has failed`, `the provided configuration file version is not supported`, `the configuration file has an invalid structure`.

### [LogType 901 — Configuration exported](/docs/mdss/configuration/syslog-message-reference#logtype-901--configuration-exported)

Identical shape with `Action="exported"`.

<110>1 2026-08-13T08:14:02.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="exported" User="jdavis" <envelope Category="4" LogType="901" UserName="jdavis">] Configuration was "exported" by "jdavis". License was included. SMTP configuration was included. Retention configuration was included. Notifications configuration was included. Users were not included
### [LogType 950 — Notification settings changed](/docs/mdss/configuration/syslog-message-reference#logtype-950--notification-settings-changed)

Message fields: `NotificationType`, `Action`, `User`.

<110>1 2026-08-13T08:30:10.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta NotificationType="Blocked file notifications" Action="enabled" User="jdavis" <envelope Category="4" LogType="950" UserName="jdavis">] "Blocked file notifications" were "enabled" by "jdavis".

`NotificationType` is one of: `Email notifications for scan reports`, `Email notifications scan reports recipients`, `Blocked file notifications`, `Blocked file notifications recipients`, `User request notifications`, `Webhook Scan completed notifications`, `Webhook Scan completed notifications details`, `Webhook File scanned notifications details`, `RabbitMq file scanned notifications details`, `Email notifications settings`, `Webhook notifications settings`, `RabbitMQ notifications settings`.

`Action` is `enabled`, `disabled` or `updated`. **Failure variant** — error severity, PRI `<107>`, `were` becomes `could not be`.

> **LogType 950 appears in two categories**
>
> With `Category="4"` it is a settings change, as above. With `Category="8"` it is a notification delivery result — see section 9. Filter on both fields together.

### [LogType 975 — SMTP configuration changed](/docs/mdss/configuration/syslog-message-reference#logtype-975--smtp-configuration-changed)

Message fields: `Action` (`enabled`, `disabled`, `updated`), `User`.

<110>1 2026-08-13T08:33:20.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="updated" User="jdavis" <envelope Category="4" LogType="975" UserName="jdavis">] SMTP configuration was "updated" by "jdavis".

**Failure variant** — error severity, PRI `<107>`, `was` becomes `could not be`.

### [LogType 1000 — External logger added](/docs/mdss/configuration/syslog-message-reference#logtype-1000--external-logger-added)

The server details are embedded in the message text. Message fields: `Action`, `User`.

<110>1 2026-08-13T10:01:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="added" User="jdavis" <envelope Category="4" LogType="1000" UserName="jdavis">] External logger (serverAddress: siem.example.com; port: 6514) was "added" by "jdavis".
### [LogType 1001 — External logger updated](/docs/mdss/configuration/syslog-message-reference#logtype-1001--external-logger-updated)

Also used when a destination is enabled or disabled, with `Action="enabled"` or `Action="disabled"`.

<110>1 2026-08-13T10:03:15.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="disabled" User="jdavis" <envelope Category="4" LogType="1001" UserName="jdavis">] External logger (serverAddress: siem.example.com; port: 6514) was "disabled" by "jdavis".
### [LogType 1002 — External logger deleted](/docs/mdss/configuration/syslog-message-reference#logtype-1002--external-logger-deleted)

`Action="removed"`.

<110>1 2026-08-13T10:05:40.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="removed" User="jdavis" <envelope Category="4" LogType="1002" UserName="jdavis">] External logger (serverAddress: siem.example.com; port: 6514) was "removed" by "jdavis".

**Failure variants** — error severity, PRI `<107>`. Six distinct messages, all with fields `User` and `Action` in present tense (`adding`, `updating`, `removing`, `enabling`, `disabling`):

| Cause | Message |
| --- | --- |
| Duplicate | `"jdavis" "adding" external logger failed because one with the same configuration already exists.` |
| Connection test failed | `"jdavis" "adding" external logger failed because the configuration is not valid.` |
| Not found | `"jdavis" "removing" external logger failed because the configuration does not exist.` |
| Already in that state | `"jdavis" "enabling" external logger failed because it was already "enabled".` |
| Limit reached | `"jdavis" "adding" external logger failed because because the maximum number of the same integration type was exceeded.` |
| Unexpected error | `"jdavis" "adding" external logger failed because an unexpected error occurred.` |

### [LogType 1100 — Data retention changed](/docs/mdss/configuration/syslog-message-reference#logtype-1100--data-retention-changed)

Message field: `User`. The detail sentence is part of the message text.

<110>1 2026-08-13T08:50:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="John Davis (jdavis)" <envelope Category="4" LogType="1100" UserName="jdavis">] Data retention configuration was successfully updated by "John Davis (jdavis)". Audit logs older than 90 days will be deleted.

Detail sentences, by action:

| Action | Success sentence | Failure sentence |
| --- | --- | --- |
| Enable report retention | `Reports retention is enabled.` | `Reports retention could not be enabled.` |
| Disable report retention | `Reports retention is disabled.` | `Reports retention could not be disabled.` |
| Change report retention days | `Reports older than 90 days will be deleted.` | `Retention days could not be updated for reports.` |
| Change audit retention days | `Audit logs older than 90 days will be deleted.` | `Retention days could not be updated for audit logs.` |
| Change RTP history retention days | `Files processed during Real-Time Processing older than 30 days will be deleted.` | `Retention days could not be updated for Real-Time Processing history.` |

On failure, severity is error, PRI `<107>`, and `was successfully` becomes `could not be`.

### [LogType 1200 to 1202 — API key changed](/docs/mdss/configuration/syslog-message-reference#logtype-1200-to-1202--api-key-changed)

The key value is truncated to its first six characters. Message fields: `TruncatedAPIKey`, `Action`, `User`.

| `LogType` | `Action` |
| --- | --- |
| `1200` | `added` |
| `1201` | `updated` |
| `1202` | `deleted` |

<110>1 2026-08-13T09:00:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta TruncatedAPIKey="a3f9c1" Action="added" User="John Davis (jdavis)" <envelope Category="4" LogType="1200" UserName="jdavis">] API Key "a3f9c1..." was "added" by "John Davis (jdavis)".

**Failure variant** — error severity, PRI `<107>`, with `FailureReason`:

<107>1 ... [meta User="John Davis (jdavis)" Action="add" TruncatedAPIKey="a3f9c1" FailureReason="an API Key with the same value already exists" <envelope Category="4" LogType="1200" UserName="jdavis">] User "John Davis (jdavis)" was unable to "add" API Key "a3f9c1" because "an API Key with the same value already exists".

Other failure reasons: `an unexpected error occurred`, `the requested user was not found`, `the requested API Key was not found`, `a key rotation is currently in progress`.

> **API key usage is not audited**
>
> These events cover the key's lifecycle only. Requests authenticated with an API key do not produce audit events.

### [LogType 1300 — SSO configuration changed](/docs/mdss/configuration/syslog-message-reference#logtype-1300--sso-configuration-changed)

**Enabled or reconfigured** — fields `User`, `SsoType`, `SsoProvider`, `Authority`:

<110>1 2026-08-13T09:05:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="John Davis (jdavis)" SsoType="Oidc" SsoProvider="AzureAd" Authority="https://login.microsoftonline.com/contoso" <envelope Category="4" LogType="1300" UserName="jdavis">] "John Davis (jdavis)" changed Single Sign-On configuration to type "Oidc", provider "AzureAd", authority "https://login.microsoftonline.com/contoso".

**Disabled** — field `User` only:

<110>1 ... [meta User="John Davis (jdavis)" <envelope Category="4" LogType="1300" UserName="jdavis">] "John Davis (jdavis)" disabled Single Sign-On configuration.

**Failure variant** — error severity, PRI `<107>`:

<107>1 ... [meta User="John Davis (jdavis)" <envelope Category="4" LogType="1300" UserName="jdavis">] "John Davis (jdavis)" tried to change the Single Sign-On configuration, but failed.
### [LogType 1410 — Workflow scanning modules changed](/docs/mdss/configuration/syslog-message-reference#logtype-1410--workflow-scanning-modules-changed)

Message fields: `WorkflowId`, `Technologies`.

<110>1 2026-08-13T09:30:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" Technologies="Antimalware, DeepCdr, VulnerabilityAssessment" <envelope Category="4" LogType="1410" UserName="jdavis">] Scanning modules for Workflow "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" have been updated. New values: "Antimalware, DeepCdr, VulnerabilityAssessment".
### [LogType 1600 — On-demand scan requested](/docs/mdss/configuration/syslog-message-reference#logtype-1600--on-demand-scan-requested)

**Single file** — file identity fields plus `UserName`:

<110>1 2026-08-13T11:20:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta fileName="invoice.docx" filePath="/finance/2026/invoice.docx" fileHash="5d41402abc4b2a76b9719d911017c592" fileSize="48213" fileId="0199c0de-7a1e-7000-8000-0000000000ab" lastModified="08/12/2026 16:40:11" UserName="jdavis" <envelope Category="4" LogType="1600" UserName="jdavis">] Successfully sent request to scan file on demand (fileName: "invoice.docx"; filePath: "/finance/2026/invoice.docx"; fileHash: "5d41402abc4b2a76b9719d911017c592"; fileSize: 48213; fileId: "0199c0de-7a1e-7000-8000-0000000000ab"; lastModified: 08/12/2026 16:40:11) . Action performed by "jdavis"

**Filtered rescan of many files** — scan fields instead of file fields:

<110>1 2026-08-13T11:22:30.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" UserName="jdavis" <envelope Category="4" LogType="1600" UserName="jdavis">] Successfully sent request to rescan multiple files on demand for (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process") . Action performed by "jdavis"
### [LogType 2000 — Encryption key event](/docs/mdss/configuration/syslog-message-reference#logtype-2000--encryption-key-event)

**Key generation** — fields `Action` and `ActionAndUser`:

<110>1 2026-08-13T02:00:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Action="Started" ActionAndUser="was started by John Davis (jdavis)" <envelope Category="4" LogType="2000" UserName="jdavis">] Key generation "was started by John Davis (jdavis)".

Completion reads `Key generation "was completed".` Failure reads `Key generation "failed".` at error severity, PRI `<107>`.

**Request cancelled during key rotation** — field `Request`:

<108>1 2026-08-13T02:00:30.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Request=" POST /api/storage" <envelope Category="4" LogType="2000" UserName="jdavis">] Request " POST /api/storage" was cancelled because a key rotation is currently in progress.
### [LogType 2200 — HTTPS certificate changed](/docs/mdss/configuration/syslog-message-reference#logtype-2200--https-certificate-changed)

Message fields: `ActionMessage`, `User`.

<110>1 2026-08-13T07:45:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta ActionMessage="enabled, and certificate was updated" User="John Davis (jdavis)" <envelope Category="4" LogType="2200" UserName="jdavis">] HTTPS was "enabled, and certificate was updated" by "John Davis (jdavis)".

Disabling reads `HTTPS was "disabled" by "John Davis (jdavis)".`

### [LogType 2300 — Telemetry configuration changed](/docs/mdss/configuration/syslog-message-reference#logtype-2300--telemetry-configuration-changed)

Message field: `Status`. Emitted by the system on startup reconciliation, or by an administrator.

<110>1 2026-08-13T07:30:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Status="enabled" <envelope Category="4" LogType="2300" UserName="jdavis">] Telemetry configuration was updated. Status: "enabled"

---

## [8. Category 6 — Users](/docs/mdss/configuration/syslog-message-reference#8-category-6--users)

`Category="6"`.

### [LogType 602 to 606 — User account changed](/docs/mdss/configuration/syslog-message-reference#logtype-602-to-606--user-account-changed)

Message fields: `Username` (the account acted on), `Action`.

| `LogType` | Event | `Action` | Message |
| --- | --- | --- | --- |
| `602` | User created | `created` | `User "mrossi" was "created".` |
| `603` | User registered | `registered` | `User "mrossi" was "registered".` |
| `604` | User role updated | `updated` | `User "mrossi"'s role was "updated".` |
| `605` | User updated | `updated` | `User "mrossi" was "updated".` |
| `605` | Password reset | `reset` | `User "mrossi"'s password was "reset".` |

<110>1 2026-08-13T09:40:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Username="mrossi" Action="created" <envelope Category="6" LogType="602" UserName="mrossi">] User "mrossi" was "created".

Role update:

<110>1 2026-08-13T09:41:15.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Username="mrossi" Action="updated" <envelope Category="6" LogType="604" UserName="mrossi">] User "mrossi"'s role was "updated".

Removal uses `LogType="606"` with `Action="removed"`.

> **Password reset shares LogType 605 with user update**
>
> Both are `LogType="605"`. Distinguish them by the message text or the `Action` field — `reset` versus `updated`.

**Failure variant** — error severity, PRI `<107>`:

<107>1 ... [meta Username="mrossi" Action="created" <envelope Category="6" LogType="602" UserName="mrossi">] User "mrossi" could not be "created".
> **The actor is the account acted on, not the administrator**
>
> On these events `UserName` and `UserId` identify the user being created, updated or removed. The administrator who performed the action appears in the message text only when MDSS has it, so do not rely on the envelope to identify the operator here.

### [LogType 1800 — Product tour finalised](/docs/mdss/configuration/syslog-message-reference#logtype-1800--product-tour-finalised)

Message fields: `UserName`, `TourType`.

<110>1 2026-08-13T09:50:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta UserName="jdavis" TourType="Onboarding" <envelope Category="6" LogType="1800" UserName="jdavis">] User "jdavis" finalized user tour "Onboarding".

---

## [9. Category 8 — Notifications](/docs/mdss/configuration/syslog-message-reference#9-category-8--notifications)

`Category="8"`. Delivery results for outbound notifications. All emitted by the system, so `UserName="system"`.

### [LogType 950 — Email notification sent](/docs/mdss/configuration/syslog-message-reference#logtype-950--email-notification-sent)

Recipients and the notification description are embedded in the message text; there are no message fields.

<110>1 2026-08-13T12:16:20.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta <envelope Category="8" LogType="950" UserName="system">] Email notification for blocked file invoice.docx was sent to: soc@example.com, ciso@example.com

Notification descriptions, by type:

| Type | Description text |
| --- | --- |
| Report generated | `Email notification that contains the scan Nightly Finance report` |
| New user registered | `Email notification for the new registered user` |
| User request processed | `Email notification after user request was processed` |
| Password reset | `Email notification that contains the password reset details` |
| Password reset completed | `Email confirmation after password reset` |
| Blocked file | `Email notification for blocked file invoice.docx` |
| User updated | `Email confirmation after user update` |
| Generic | `Email notification` |

**Partial delivery failure** — the message names both sets of recipients:

<110>1 ... [meta <envelope Category="8" LogType="950" UserName="system">] Email notification for blocked file invoice.docx was sent to: soc@example.com Email could not be sent to: ciso@example.com

**Total delivery failure** — error severity, PRI `<107>`:

<107>1 ... [meta <envelope Category="8" LogType="950" UserName="system">] Email notification for blocked file invoice.docx could not be sent to: soc@example.com, ciso@example.com

**No recipient configured** — error severity, PRI `<107>`:

<107>1 ... [meta <envelope Category="8" LogType="950" UserName="system">] Email notification for blocked file invoice.docx could not be sent. The recipient could not be found.
### [LogType 950 — Webhook notification sent](/docs/mdss/configuration/syslog-message-reference#logtype-950--webhook-notification-sent)

Message field: `ScanName` or `FileName`.

<110>1 2026-08-13T12:16:25.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta ScanName="Nightly Finance" <envelope Category="8" LogType="950" UserName="system">] Webhook notification for completion of scan "Nightly Finance" was successfully sent<110>1 2026-08-13T12:16:26.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta FileName="invoice.docx" <envelope Category="8" LogType="950" UserName="system">] Webhook notification for scanned file "invoice.docx" was successfully sent

**Failure variants** — error severity, PRI `<107>`: `Failed to send webhook notification for scan "Nightly Finance"` and `Failed to send webhook notification for scanned file "invoice.docx"`.

### [LogType 950 — Message-queue notification sent](/docs/mdss/configuration/syslog-message-reference#logtype-950--message-queue-notification-sent)

Message field: `FileName`.

<110>1 2026-08-13T12:16:27.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta FileName="invoice.docx" <envelope Category="8" LogType="950" UserName="system">] RabbitMQ notification for scanned file "invoice.docx" was successfully sent

**Failure variant** — error severity, PRI `<107>`: `Failed to send RabbitMQ notification for scanned file "invoice.docx"`.

### [LogType 1700 — Report generated](/docs/mdss/configuration/syslog-message-reference#logtype-1700--report-generated)

Message fields: scan fields.

<110>1 2026-08-13T12:20:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta scanId="e1b6d842-0f37-4c9b-8a15-63d0947fe2ba" scanName="Nightly Finance" scanType="Scheduled Process" <envelope Category="8" LogType="1700" UserName="system">] PDF Report of scan (ID: "e1b6d842-0f37-4c9b-8a15-63d0947fe2ba", name: "Nightly Finance", type: "Scheduled Process") has been created

---

## [10. Category 9 — Group units](/docs/mdss/configuration/syslog-message-reference#10-category-9--group-units)

`Category="9"`.

### [LogType 320 to 322 — Group added, updated, removed](/docs/mdss/configuration/syslog-message-reference#logtype-320-to-322--group-added-updated-removed)

Message fields: `groupName`, `groupId`, `Action`, `User`.

| `LogType` | `Action` |
| --- | --- |
| `320` | `added` |
| `321` | `updated` |
| `322` | `removed` |

<110>1 2026-08-13T09:15:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta groupName="Finance shares" groupId="4e7c9105-8d26-4a3f-b012-75ea3c6f81db" Action="added" User="jdavis" <envelope Category="9" LogType="320" UserName="jdavis">] Group (name: "Finance shares"; ID: "4e7c9105-8d26-4a3f-b012-75ea3c6f81db") was "added" by "jdavis".

**Failure variant** — error severity, PRI `<107>`, `was` becomes `could not be`.

---

## [11. Category 10 — Account units](/docs/mdss/configuration/syslog-message-reference#11-category-10--account-units)

`Category="10"`.

### [LogType 330 to 332 — Account added, updated, removed](/docs/mdss/configuration/syslog-message-reference#logtype-330-to-332--account-added-updated-removed)

Message fields: `accountName`, `accountId`, `Action`, `User`.

| `LogType` | `Action` |
| --- | --- |
| `330` | `added` |
| `331` | `updated` |
| `332` | `removed` |

<110>1 2026-08-13T09:17:30.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta accountName="contoso-svc" accountId="6f18b3d4-9e07-42ca-8b53-1d904af7e26c" Action="added" User="jdavis" <envelope Category="10" LogType="330" UserName="jdavis">] Account (name: "contoso-svc"; ID: "6f18b3d4-9e07-42ca-8b53-1d904af7e26c") was "added" by "jdavis".

**Failure variant** — error severity, PRI `<107>`, `was` becomes `could not be`.

---

## [12. Category 11 — Remediations](/docs/mdss/configuration/syslog-message-reference#12-category-11--remediations)

`Category="11"`. Changes to remediation rules. Rule *execution* appears in category 1.

### [LogType 2101 to 2103 — Remediation rule added, updated, deleted](/docs/mdss/configuration/syslog-message-reference#logtype-2101-to-2103--remediation-rule-added-updated-deleted)

Message fields: `Type`, `HandlingType`, `WorkflowId`, `WorkflowName`, `Action`, `UserName`.

| `LogType` | `Action` |
| --- | --- |
| `2101` | `added` |
| `2102` | `updated` |
| `2103` | `deleted` |

<110>1 2026-08-13T09:35:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta Type="BlockedFileRemediation" HandlingType="Move" WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" WorkflowName="Default workflow" Action="added" UserName="jdavis" <envelope Category="11" LogType="2101" UserName="jdavis">] Remediation of type "BlockedFileRemediation" with "Move" action for Workflow (Id: "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8"; Name: "Default workflow") was "added" by "jdavis".

`Type` is one of `FileTagging`, `BlockedFileRemediation`, `AllowedFileRemediation`, `AllowedSanitizedFileRemediation`, `BlockedSanitizedFileRemediation`, `DiscoveredFileRemediation`, `DeepCdr`, `DeleteEmptyFoldersRemediation`, `ScanFileVersions`. `HandlingType` is `Move`, `Copy`, `Delete`, `Keep` or `NotApplicable`.

**Rule disabled** — no `HandlingType`:

<110>1 ... [meta Type="BlockedFileRemediation" WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" WorkflowName="Default workflow" UserName="jdavis" <envelope Category="11" LogType="2102" UserName="jdavis">] Remediation of type "BlockedFileRemediation" was disabled for Workflow (Id: "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8"; Name: "Default workflow") by "jdavis".

**Empty-folder remediation** — adds a `Depth` field:

<110>1 ... [meta Type="DeleteEmptyFoldersRemediation" WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" WorkflowName="Default workflow" Depth="3" Action="added" UserName="jdavis" <envelope Category="11" LogType="2101" UserName="jdavis">] Remediation of type "DeleteEmptyFoldersRemediation" for Workflow (Id: "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8"; Name: "Default workflow") with folder depth: 3 was "added" by "jdavis".

**Failure variant** — error severity, PRI `<107>`:

<107>1 ... [meta Type="BlockedFileRemediation" WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" WorkflowName="Default workflow" <envelope Category="11" LogType="2101" UserName="jdavis">] Unable to use remediation of "BlockedFileRemediation" for Workflow (Id: "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8"; Name: "Default workflow")

---

## [13. Category 12 — Workflows](/docs/mdss/configuration/syslog-message-reference#13-category-12--workflows)

`Category="12"`.

### [LogType 1400 to 1404 — Workflow changed](/docs/mdss/configuration/syslog-message-reference#logtype-1400-to-1404--workflow-changed)

Message fields: `WorkflowId`, `WorkflowName`, `Action`, `UserName`, and — except on delete — `FileDefinitionMode`.

| `LogType` | `Action` |
| --- | --- |
| `1400` | `added` |
| `1401` | `updated` |
| `1402` | `deleted` |
| `1403` | `set as default` |
| `1404` | `imported` |

<110>1 2026-08-13T09:32:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta WorkflowId="9d4e1f60-3a72-4b85-8c19-f2073be5a1c8" WorkflowName="Default workflow" Action="added" UserName="jdavis" FileDefinitionMode="Strict" <envelope Category="12" LogType="1400" UserName="jdavis">] Workflow (Id: "9d4e1f60-3a72-4b85-8c19-f2073be5a1c8"; Name: "Default workflow") was "added" by "jdavis". File Definition: mode - "Strict"

With the configurable blocking strategy, `FileDefinitionMode="Configurable"` and the message lists the individual blocking options.

**Failure variant** — error severity, PRI `<107>`, with `ErrorMessage`:

<107>1 ... [meta Action="add" Workflow="Default workflow" ErrorMessage="A workflow with this name already exists" UserName="jdavis" FileDefinitionMode="Strict" <envelope Category="12" LogType="1400" UserName="jdavis">] Unable to "add" Workflow "Default workflow". Response message: "A workflow with this name already exists". Action performed by "jdavis". File Definition: mode - "Strict"

---

## [14. Category 13 — Access control](/docs/mdss/configuration/syslog-message-reference#14-category-13--access-control)

`Category="13"`. Role and permission assignment. Message field: `User`. The description is part of the message text.

### [LogType 2400 to 2412](/docs/mdss/configuration/syslog-message-reference#logtype-2400-to-2412)

| `LogType` | Event | Success message | Failure message |
| --- | --- | --- | --- |
| `2400` | Role assigned | `Role was assigned to a user by "John Davis (jdavis)".` | `Role could not be assigned to a user by "John Davis (jdavis)".` |
| `2401` | Role removed | `Role was removed from a user by "John Davis (jdavis)".` | `Role could not be removed from a user by "John Davis (jdavis)".` |
| `2402` | Custom role created | `Custom role was created by "John Davis (jdavis)".` | `Custom role could not be created by "John Davis (jdavis)".` |
| `2403` | Custom role deleted | `Custom role was deleted by "John Davis (jdavis)".` | `Custom role could not be deleted by "John Davis (jdavis)".` |
| `2410` | Permission assigned | `Permission was assigned to a user by "John Davis (jdavis)".` | `Permission could not be assigned to a user by "John Davis (jdavis)".` |
| `2411` | Permission removed | `Permission was removed from a user by "John Davis (jdavis)".` | `Permission could not be removed from a user by "John Davis (jdavis)".` |
| `2412` | Roles replaced | `Roles were replaced for a user by "John Davis (jdavis)".` | `Roles could not be replaced for a user by "John Davis (jdavis)".` |

<110>1 2026-08-13T09:45:00.000000+02:00 mdss-prod-01 MetaDefenderStorageSecurity 27725 - [meta User="John Davis (jdavis)" <envelope Category="13" LogType="2400" UserName="jdavis">] Role was assigned to a user by "John Davis (jdavis)".

Failure variants are emitted at error severity, PRI `<107>`.

> **The affected user is not a field**
>
> These events name the administrator who made the change, not the user whose access changed. The target user is not carried on the event.

---

## [15. Reserved event types](/docs/mdss/configuration/syslog-message-reference#15-reserved-event-types)

The schema defines 112 event types. The 14 below are reserved and are **not** emitted by MDSS 4.5. Do not build rules that depend on them.

| `LogType` | Reserved name |
| --- | --- |
| `201` | File sanitized, original kept |
| `203` | File sanitized, original deleted |
| `204` | File decryption |
| `350` | Security checklist item |
| `351` | Security checklist verified |
| `410` | File tagging |
| `411` | Deep CDR remediation |
| `412` | Sanitized files remediation |
| `413` | Blocked files remediation |
| `414` | Treat files with sensitive data as blocked |
| `415` | Treat files with vulnerabilities as blocked |
| `416` | Allowed files remediation |
| `417` | Strict block files strategy |
| `418` | Configurable block files strategy |

Category `7` (security checklist) is reserved for the same reason, and category `5` is not defined.

Parsers should handle unrecognised `LogType` and `Category` values without failing — new values may be added in later releases.

---

## [16. Quick index](/docs/mdss/configuration/syslog-message-reference#16-quick-index)

| `LogType` | Event | Category |
| --- | --- | --- |
| `0` | File discovered | 0 |
| `1` | File scanned | 0 |
| `2` | File discovery failed or skipped | 0 |
| `3` | File cancelled | 0 |
| `100` | Scan process started | 0 |
| `101` | Scan process completed | 0 |
| `102` | Scan process cancelled | 0 |
| `103` | Scan process failed | 0 |
| `200` | File tagged | 1 |
| `205` | Blocked file moved | 1 |
| `206` | Blocked file deleted | 1 |
| `207` | Sanitized file moved | 1 |
| `208` | Allowed file moved | 1 |
| `209` | Blocked file copied | 1 |
| `210` | Sanitized file copied | 1 |
| `211` | Allowed file copied | 1 |
| `212` | Blocked file kept | 1 |
| `213` | Allowed file kept | 1 |
| `214` | Sanitized file kept | 1 |
| `215` | Allowed file deleted | 1 |
| `216` | File versions scanned | 1 |
| `217` | Discovered file deleted | 1 |
| `218` | Discovered file moved | 1 |
| `219` | Discovered file copied | 1 |
| `220` | Discovered file kept | 1 |
| `221` | Sanitized file deleted | 1 |
| `300` | Storage added | 2 |
| `301` | Storage updated | 2 |
| `302` | Storage removed | 2 |
| `320` | Group added | 9 |
| `321` | Group updated | 9 |
| `322` | Group removed | 9 |
| `330` | Account added | 10 |
| `331` | Account updated | 10 |
| `332` | Account removed | 10 |
| `400` | Real-time processing changed | 2 |
| `419` | Empty folders deleted | 1 |
| `600` | Signed in | 3 |
| `601` | Signed out | 3 |
| `602` | User created | 6 |
| `603` | User registered | 6 |
| `604` | User role updated | 6 |
| `605` | User updated or password reset | 6 |
| `606` | User removed | 6 |
| `700` | Scan instance added | 4 |
| `701` | Scan instance updated | 4 |
| `702` | Scan instance deleted | 4 |
| `703` | Scan instance imported | 4 |
| `750` | Scan pool added | 4 |
| `751` | Scan pool updated | 4 |
| `752` | Scan pool deleted | 4 |
| `753` | Scan pool imported | 4 |
| `800` | Licence activated online | 4 |
| `801` | Licence activated offline | 4 |
| `802` | Licence deactivated | 4 |
| `900` | Configuration imported | 4 |
| `901` | Configuration exported | 4 |
| `950` | Notification settings changed | 4 |
| `950` | Notification delivery result | 8 |
| `975` | SMTP configuration changed | 4 |
| `1000` | External logger added | 4 |
| `1001` | External logger updated, enabled or disabled | 4 |
| `1002` | External logger deleted | 4 |
| `1100` | Data retention changed | 4 |
| `1200` | API key added | 4 |
| `1201` | API key updated | 4 |
| `1202` | API key deleted | 4 |
| `1300` | SSO configuration changed | 4 |
| `1400` | Workflow added | 12 |
| `1401` | Workflow updated | 12 |
| `1402` | Workflow deleted | 12 |
| `1403` | Workflow set as default | 12 |
| `1404` | Workflow imported | 12 |
| `1410` | Workflow scanning modules changed | 4 |
| `1500` | Scan added | 0 |
| `1501` | Scan updated | 0 |
| `1502` | Scan deleted | 0 |
| `1503` | Scan imported | 0 |
| `1600` | On-demand scan requested | 4 |
| `1700` | Report generated | 8 |
| `1800` | Product tour finalised | 6 |
| `1900` | Scan schedule added | 0 |
| `1901` | Scan schedule updated | 0 |
| `1902` | Scan schedule deleted | 0 |
| `1903` | Scan schedule imported | 0 |
| `1904` | Scan schedule skipped | 0 |
| `2000` | Encryption key event | 4 |
| `2101` | Remediation rule added | 11 |
| `2102` | Remediation rule updated | 11 |
| `2103` | Remediation rule deleted | 11 |
| `2200` | HTTPS certificate changed | 4 |
| `2300` | Telemetry configuration changed | 4 |
| `2400` | Role assigned | 13 |
| `2401` | Role removed | 13 |
| `2402` | Custom role created | 13 |
| `2403` | Custom role deleted | 13 |
| `2410` | Permission assigned | 13 |
| `2411` | Permission removed | 13 |
| `2412` | Roles replaced | 13 |
