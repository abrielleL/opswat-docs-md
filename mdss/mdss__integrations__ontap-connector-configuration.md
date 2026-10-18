<!-- source: https://www.opswat.com/docs/mdss/integrations/ontap-connector-configuration -->

# ONTAP Connector Configuration file

The OPSWAT ONTAP Connector is the Windows service (`opswat-ontap-connector`) that sits between a NetApp ONTAP Vscan (AV) connector and a MetaDefender Storage Security (MDSS) instance. It receives scan requests from ONTAP over MSRPC named pipes, forwards each file to MDSS for real-time processing, and returns the verdict back to ONTAP.

All of its behaviour is driven by a single `config.ini` file. This page documents every section, key, accepted value and default.

---

## File location and load behaviour

|  |  |
| ---- | ---- |
| File name | `config.ini` |
| Location | The folder containing `OPSWAT-ONTAP-Connector.exe` |
| Installed location | `C:\ProgramData\OPSWAT-ONTAP-Connector\config.ini` |
| When it is read | Once, at process start, before any other initialization |
| Applying a change | **Restart the opswat-ontap-connector service.** The file is never re-read at runtime. The only exception is the `[Storage Unit N]` sections and the `StorageUnits` count, which the connector itself rewrites while running (see `StorageSyncIntervalInSeconds`). |

`config.ini` is copied from the executable folder into the installation folder by `--install` and `--upgrade`, so edit the *installed* copy when tuning a deployed connector.

Only a few values can stop the connector from starting: `IP`, `Port`, `Apikey`, `StorageUnits`, and the keys inside the `[Storage Unit N]` sections. If the file cannot be read, or one of these values is missing, empty or fails validation, the connector logs `Error when reading config.ini file` at `Fatal` level and exits without starting. Every other key falls back to its default when its value cannot be used, and the connector logs a warning and starts.

### Format rules

Standard INI semantics apply:

- Sections are declared as `[Section Name]`; section and key names are matched case-insensitively by Windows.
- Entries are `Key=Value`. Whitespace around the `=` is trimmed.
- Lines beginning with `;` are comments.
- Do **not** quote values — quotes become part of the value.
- A single value is limited to 254 characters; anything longer is truncated.
- A `[Settings]` key the connector does not recognise is ignored silently. A misspelled key therefore shows up as the setting having no effect, not as a startup error — check the effective values in the startup log line described under [What the connector logs at startup](#what-the-connector-logs-at-startup).

---

## Section `[MetaDefender Storage Security]`

Identifies the MDSS instance the connector talks to.

| Key | Required | Type | Default | Accepted values |
| ---- | ---- | ---- | ---- | ---- |
| `IP` | Yes | IPv4 address | — | Dotted-quad IPv4 only, e.g. `10.0.0.15` |
| `Port` | Yes | Integer | — | MDSS HTTP port, `1` – `65535`, e.g. `80`, `8008` |
| `PortSsl` | No | Integer | `443` | MDSS HTTPS port, `1` – `65535` |
| `IgnoreCertErrors` | No | Integer | `0` | `0` or `1` |
| `Apikey` | Yes | String | — | MDSS API key |
| `StorageUnits` | Yes | Integer | — | `0` or greater |

### `IP`

The address of the MDSS instance. **Validated against an IPv4 regular expression — hostnames. FQDNs and IPv6 addresses are rejected** and cause a fatal configuration error at startup.

### `Port` and `PortSsl`

`Port` has no default: an empty or non-numeric value, or a value outside `1` – `65535`, is a fatal configuration error. The `80` in the template is a starting value, not a default. `PortSsl` falls back to `443` when its value is non-numeric or outside `1` – `65535`, and the connector logs a warning.

The connector does not require you to declare whether MDSS is served over HTTP or HTTPS. It starts every session on plain HTTP against `Port`, and switches transport automatically:

1. A request fails with a transport-level WinHTTP error: connection reset (`12030`), an invalid server response (`12152`), the port refusing connections (`12029`), or, on a plain-HTTP request only, a TLS handshake failure (`12175`).
2. The connector flips its transport mode (HTTP ⟷ HTTPS) and retries the request once on the other port. The switch is logged at `Warning` level (`MDSS request failed with a transport error. Switched transport to …`).
3. If the retry succeeds, the new mode is kept for subsequent requests. If the retry fails as well, MDSS is treated as unreachable rather than moved, and the previous mode is restored (`The retry failed as well, so MDSS is unreachable rather than moved. Transport reverted to …`).

The switch is bidirectional and self-healing, so an MDSS instance that moves from HTTP to HTTPS (or back) is picked up without restarting the connector. Automatic switching is always on. A `PortSsl` value of `0` does not turn it off: `0` is outside the valid range, so the connector uses `443`.

A certificate failure on an HTTPS request never makes the connector switch to plain HTTP, because the retry would send the API key and the file content unencrypted. Install a certificate the connector's host trusts, or see `IgnoreCertErrors`.

The connector negotiates TLS 1.2 and, where the build environment supports it, TLS 1.3.

### `IgnoreCertErrors`

| Value | Behaviour |
| ---- | ---- |
| `0` (default) | Full TLS certificate validation. A certificate MDSS cannot prove is trusted fails the request. |
| `1` | Certificate errors are ignored on HTTPS requests: unknown CA, wrong certificate usage, host-name mismatch, and expired/not-yet-valid dates. |

Set this to `1` when MDSS is serving its default self-signed certificate. Any other value (for example `2`) falls back to `0`, full validation, and the connector logs a warning. The setting has no effect on plain HTTP requests.

> Security note: `IgnoreCertErrors=1` disables certificate validation entirely and leaves the channel open to an on-path attacker. Use it only on trusted management networks, or install a certificate the connector's host trusts.

### `Apikey`

The MDSS API key, sent as the `Apikey` HTTP header on every call the connector makes (`POST /api/webhook/realtime`, `GET /api/file/{correlationId}`, `GET /api/health`, `GET /api/account`).

This will be automatically added when you download and install the OPSWAT ONTAP Connector from MDSS. `Apikey` is required: an empty value stops the connector from starting.

The storage synchronisation reads the NetApp ONTAP accounts through `GET /api/account`, so the key must have read permission on accounts:

- Without that permission, MDSS refuses the request and every synchronisation cycle is skipped (`StorageSyncMonitor: could not enumerate storages from MDSS, skipping this cycle`). Nothing is added or removed.
- With that permission, MDSS leaves out of its answer every storage the key has no access to. Such a storage is not added, and a storage unit already written for it is removed after three cycles.

### `StorageUnits`

The number of `[Storage Unit N]` sections that follow. Must be an integer of `0` or greater; a negative number or a non-numeric value is a fatal configuration error.

`StorageUnits=0` is a valid state: it means no NetApp ONTAP storage currently has event-based real-time protection running. A connector downloaded from MDSS starts at `1`, with a `[Storage Unit 1]` section for the storage it was downloaded for. The connector then raises or lowers the count itself as storages are synchronised from MDSS.

The connector reads exactly the sections `[Storage Unit 1]` … `[Storage Unit <StorageUnits>]`. **Numbering must be consecutive and start at 1.** A gap in the numbering, or a count higher than the number of sections, makes the connector look for a section that does not exist, and the connector does not start. Sections beyond the declared count are ignored.

---

## Section `[Storage Unit N]`

One section per storage unit, numbered `1` to `StorageUnits`. Both keys are required in every section, and an empty value stops the connector from starting.

| Key | Required | Type | Default | Description |
| ---- | ---- | ---- | ---- | ---- |
| `ClientId` | Yes | String | — | The MDSS storage client id |
| `SharePath` | Yes | String | — | ONTAP-side path prefix for this storage unit |

### Storage units are maintained automatically

The connector keeps the configuration file in step with MDSS: every `StorageSyncIntervalInSeconds` it reads the NetApp ONTAP accounts and their storages from MDSS, keeps the storages whose event-based real-time protection is running, and rewrites the `[Storage Unit N]` sections and the `StorageUnits` count to match. It also adds the SVM host of each protected storage as a `data-lif::<host>` value under `HKLM\SOFTWARE\WOW6432Node\Data ONTAP\Clustered Data ONTAP Antivirus Connector\v1.0\data-lifs`, and removes the value again when no protected storage uses that host any more.

- A storage that starts event-based real-time protection in MDSS is added on the next cycle. `SharePath` is built from the account's SVM host and the storage's share name.
- An edited share path or a changed account SVM host is applied on the next cycle.
- A storage that stops event-based real-time protection, or is deleted, is removed once it has been missing from three consecutive cycles. A single short answer from MDSS is not treated as a deletion.
- If MDSS cannot be read (unreachable, non-200 response, unparseable payload), the cycle is skipped and nothing is removed.
- Changes apply to the running configuration immediately. No service restart is needed.

Storages protected by polling real-time protection are handled by MDSS directly and are left out of `config.ini`.

Hand-written `[Storage Unit N]` sections are still accepted. They are kept as long as the synchronisation is disabled (`StorageSyncIntervalInSeconds=0`). With the synchronisation enabled, a hand-written section whose storage is not reported by MDSS as event-based-RTP active is removed after three cycles.

### `ClientId`

The client id of the storage configured in MDSS. It is sent as `storageClientId` in the real-time webhook payload and tells MDSS which storage the file belongs to. Copy it from the storage's configuration in MDSS.

### `SharePath`

The ONTAP path prefix that identifies files belonging to this storage unit, for example `svm1\share1`. The value is used twice on each incoming scan request:

1. **Storage-unit selection.** The connector strips the `\\?\UNC\` prefix from the path ONTAP sent and looks for the storage unit whose `SharePath` matches the start of what remains. The match is case-insensitive and must end at a path separator: `svm1\share` does not claim a file under `svm1\share_2`. When several units match (nested share paths), the longest `SharePath` wins. If no unit matches, the file is dropped with `Failed to find a MDSS storage unit for file …` at `Error` level and ONTAP never receives a verdict for it.
2. **Computing the MDSS-relative path.** The connector strips `SharePath` plus one separator from the front of the path that remains after the `\\?\UNC\` prefix. The result is the relative path sent to MDSS as the file's `name`.

Because step 2 removes a fixed number of characters, `SharePath` must be **the exact leading portion of the ONTAP path after \\?\UNC\** — not merely a substring that happens to appear somewhere in it. A value that is too short or too long produces a wrong relative path and MDSS will not find the file.

Leading backslashes are stripped when the value is read, so `\svm1\share1` and `svm1\share1` are equivalent. Do not add a trailing separator. Share paths written by the synchronisation are normalised the same way.

---

## Section `[Settings]`

Every key in this section is optional, and no value in it can stop the connector from starting:

- A missing or empty key uses its default.
- A non-numeric value, or a value outside the key's range, also uses the default. The connector logs a warning that names the key, the valid range and the default it used, for example:

```plaintext
Value out of range for key ZoneIdentifierFiles. Valid range: [0,3]. Using the default: 0
Invalid value (must be an integer) for key ZoneIdentifierFiles. Valid range: [0,3]. Using the default: 0
```

The values in effect are shown in the configuration dump described under [What the connector logs at startup](#what-the-connector-logs-at-startup).

| Key | Type | Default | Range / accepted values |
| ---- | ---- | ---- | ---- |
| `LogRetentionCountInFiles` | Integer | `7` | `1` – `200` |
| `LogMaxFileSizeInMegabytes` | Integer | `10` | `1` – `1024` |
| `LogPath` | String | empty (`<install dir>\logs`) | An absolute or relative directory path, or empty |
| `LogLevel` | String | `Information` | `Verbose`, `Debug`, `Information`, `Warning`, `Error`, `Fatal` |
| `FileProcessingTimeoutInSeconds` | Integer | `3600` | `1` or greater |
| `RpcLocalPipeHost` | String | `127.0.0.1` | An address, or the literal `NULL` |
| `ZoneIdentifierFiles` | Integer | `0` | `0` – `3` |
| `TimeoutResponse` | Integer | `4` | `0` – `5` |
| `StorageSyncIntervalInSeconds` | Integer | `15` | `0` – `86400`; `0` disables the synchronisation |

### `LogRetentionCountInFiles`

How many log files to keep. A rotation thread runs every 10 seconds and deletes the oldest of the connector's own log files until only `LogRetentionCountInFiles` remain. Each deletion is logged as `LogRotation - File deleted. File: <name>`.

Retention only ever counts and deletes files the connector itself named — `YYYYMMDD.log`, `YYYYMMDD_HHMMSS.log` and `YYYYMMDD_HHMMSS_<n>.log` — so a `LogPath` directory that also holds other content is safe.

A value outside `1` – `200` falls back to `7`, with the warning `Value out of range for key LogRetentionCountInFiles. Valid range: [1,200]. Using the default: 7`.

> **Upgrading from a version earlier than 4.6.0**
>
> `LogRetentionCountInDays` is the previous name of this key. Retention has always counted files, not days; the key was renamed to say so. A `config.ini` that still uses `LogRetentionCountInDays` keeps working: when `LogRetentionCountInFiles` is absent or empty, the value of `LogRetentionCountInDays` is applied to the file count, and a fallback warning names the key that was actually read. When both keys are present, `LogRetentionCountInFiles` wins.

### `LogMaxFileSizeInMegabytes`

The size at which the current log file is rolled over. The connector writes one file per day, named `YYYYMMDD.log`. When that file reaches `LogMaxFileSizeInMegabytes`, logging continues in a new file named `YYYYMMDD_HHMMSS.log` (`YYYYMMDD_HHMMSS_<n>.log` when several rolls happen in the same second). The previous file is kept and is not appended to again; `LogRetentionCountInFiles` then bounds how many files remain.

An identical warning or error is written **once per log file**. A scanned file that is retried until its processing timeout produces one line rather than one per attempt. The suppression resets each time logging moves to a new log file, at the size limit and at the change of day, so every log file still carries the error at least once. It also resets after 5,000 distinct warnings and errors, so a repeated line can appear again in the same log file.

A value outside `1` – `1024` falls back to `10`, with the warning `Value out of range for key LogMaxFileSizeInMegabytes. Valid range: [1,1024]. Using the default: 10`.

### `LogPath`

The directory the log files are written to. Leave it empty to keep the default `logs` folder next to the executable — `C:\ProgramData\OPSWAT-ONTAP-Connector\logs` for an installed connector. A directory that does not exist yet is created.

A relative path is resolved against the installation directory, not against the service's working directory. For example, `LogPath=connector-logs` on an installed connector writes to `C:\ProgramData\OPSWAT-ONTAP-Connector\connector-logs`. The resolved path is logged once at `Information` level: `Configured LogPath is relative, resolved against the installation directory: <path>`.

If the configured path cannot be used — for example a drive that does not exist, or a directory the service account cannot write to — the service still starts. Logging falls back to the default directory and one line at `Error` level records the configured path and an error code: `Configured LogPath cannot be used, logging to <default> instead. Configured path: <value>`. The code is:

- `5`, the Windows access-denied code, when the service account cannot create the directory.
- `-6` when the directory cannot be created for another reason, for example a drive that does not exist.
- `-11` when the directory exists but the log file cannot be opened in it.

### `LogLevel`

The minimum severity written to the log. Messages below the configured level are discarded.

| Value | Use |
| ---- | ---- |
| `Verbose` | Everything, including per-file ONTAP verdict mapping |
| `Debug` | Full HTTP request and response bodies exchanged with MDSS — the level to use when troubleshooting MDSS connectivity |
| `Information` (default) | Lifecycle events, per-file progress, configuration dump at startup |
| `Warning` | Transport switches, ONTAP service not yet available, non-fatal failures |
| `Error` | Failed operations |
| `Fatal` | Startup-blocking failures only |

**The value is compared case-sensitively**, so it must be spelled exactly as listed. Any other value, including `information`, falls back to `Information`, with the warning `Invalid LogLevel value: information. Available options: Verbose, Debug, Information, Warning, Error, Fatal. Using the default: Information`.

Note that the level only takes effect once the service main thread starts; configuration parsing itself is logged at `Verbose`, which is why the startup banner and the configuration dump always appear.

When the executable is run interactively (`--install`, `--uninstall`, `--upgrade`) output goes to the console instead of a file. File logging is used for `--service` and `--debug`.

### `FileProcessingTimeoutInSeconds`

How long a single file may stay in the connector's pipeline, measured from the moment ONTAP's scan request was received. When the timeout is exceeded and MDSS has still not returned a final verdict — or the connector cannot reach MDSS or ONTAP at all — the connector gives up on the file: it sends the verdict configured in `TimeoutResponse` to ONTAP and removes the file from its tracking list. Exactly one timeout verdict is sent per file.

The default `3600` (one hour) is deliberately generous: it must accommodate the slowest case MDSS can produce, including large archives and Deep CDR. Lowering it makes the connector give up sooner on files MDSS is still working on. The minimum is `1` and there is no upper bound. A lower or non-numeric value falls back to `3600`, with the warning `Value out of range for key FileProcessingTimeoutInSeconds. Minimum: 1. Using the default: 3600`.

Files still in flight are persisted to `data.json` next to the executable every 3 seconds, so a connector restart does not lose pending work; the timeout continues to be measured from the original request time.

### `RpcLocalPipeHost`

The network address the connector uses when binding to the NetApp registration pipe (`\pipe\ntapvscp`) exposed by the ONTAP AV connector service (`ontapavc`) on the same machine.

| Value | Behaviour |
| ---- | ---- |
| `127.0.0.1` (default) | Binds the named pipe using the loopback address |
| Any other address | Binds using that address as the network address |
| `NULL` (the literal four-character string) | Binds with a null network address — the local machine, with no explicit host |

Use `NULL` when the loopback binding is refused by the local RPC configuration. The connector retries the binding and the ONTAP registration every 3 seconds until both succeed, so a wrong value shows up as a repeating `RpcConnectionThread: Failed to create connection` or `Failed to register to RPC server` in the log.

### `ZoneIdentifierFiles`

Controls how `:Zone.Identifier` alternate-data-stream files are handled. Windows creates these tiny metadata streams alongside downloaded files, and ONTAP submits them for scanning like any other file — which can double the request volume for no security benefit.

| Value | Mode | Behaviour |
| ---- | ---- | ---- |
| `0` | Skip (default) | The request is logged and dropped. No scan, and **no verdict is returned to ONTAP** — ONTAP applies its own scan-request timeout policy. |
| `1` | Scan | Treated as a normal file and sent to MDSS through the usual pipeline. |
| `2` | Allow | An immediate allow verdict (`VSENGINE_NO_ERROR`) is returned without scanning. |
| `3` | Block | An immediate block verdict (`VSENGINE_INFECTED`) is returned without scanning. |

A value outside `0` – `3` falls back to `0` (Skip), and the connector logs a warning.

Prefer `2` (Allow) over `0` (Skip) if ONTAP clients are seeing access delays on downloaded files: it settles the request immediately instead of leaving ONTAP waiting for its own timeout.

### `TimeoutResponse`

The verdict sent to ONTAP when a file hits `FileProcessingTimeoutInSeconds`. Each value maps to a NetApp Vscan engine status, and it is ONTAP — not the connector — that decides what the client sees based on that status and the share's `scan-mandatory` setting.

| Value | Mode | ONTAP status | Effect |
| ---- | ---- | ---- | ---- |
| `0` | Allow | `VSENGINE_NO_ERROR` | Access is allowed. The file is treated as clean. |
| `1` | TimeoutNoBlock | `VSENGINE_INTERNAL_TIMEOUT_NOBLOCK` | Access is allowed, but recorded as a scanner timeout. |
| `2` | InfectedBlock | `VSENGINE_INFECTED` | Access is always blocked and the file is reported as infected. |
| `3` | TimeoutBlock | `VSENGINE_INTERNAL_TIMEOUT_BLOCK` | Access is always blocked, with a timeout reason. |
| `4` | Timeout (default) | `VSENGINE_INTERNAL_TIMEOUT` | Blocked only where scanning is mandatory; allowed otherwise. |
| `5` | EngineBusyRetryLater | `VSENGINE_BUSY_TRY_AGAIN_LATER` | Reported as scanner busy so ONTAP can retry or hand the request to another scanner. |

A value outside `0` – `5` falls back to `4` (Timeout), and the connector logs a warning. Use `0` or `1` for availability-first deployments, `2` or `3` for security-first, and `5` when several scanners serve the same ONTAP cluster and another one should get a chance at the file.

### `StorageSyncIntervalInSeconds`

How often, in seconds, the connector synchronises its storage units with MDSS. Each cycle reads the NetApp ONTAP accounts and their storages from MDSS (`GET /api/account`), keeps the storages whose event-based real-time protection is running, and reconciles two places against that answer: the `[Storage Unit N]` sections in `config.ini`, and the `data-lif::<host>` values in the ONTAP AV Connector registry. The full behaviour is described under [Storage units are maintained automatically](#storage-units-are-maintained-automatically).

`0` turns the synchronisation off. No cycle runs, `config.ini` and the `data-lifs` registry values are left exactly as configured by hand, and the startup log states `Storage synchronisation is disabled (StorageSyncIntervalInSeconds=0)`. Use this when the storage units are managed by another tool, or as a kill switch.

A value outside `0` – `86400` falls back to `15`, with the warning `Value out of range for key StorageSyncIntervalInSeconds. Valid range: [0,86400]. Using the default: 15`. Only the exact value `0` turns the synchronisation off; a negative value leaves it running every 15 seconds.

---

## Complete example

```ini
[MetaDefender Storage Security]
IP=10.0.0.15
Port=8008
PortSsl=8443
IgnoreCertErrors=1
Apikey=b1946ac92492d2347c6235b4d2611184
StorageUnits=2

[Storage Unit 1]
ClientId=6f1c2f7a-6c1e-4f9a-9c0e-3ac0d1f2b111
SharePath=svm1\finance_share

[Storage Unit 2]
ClientId=9d4b8e01-11aa-42cc-8e77-5b6c9d0e2222
SharePath=svm1\hr_share

[Settings]
LogRetentionCountInFiles=14
LogMaxFileSizeInMegabytes=50
LogPath=D:\mdss-connector-logs
LogLevel=Debug
FileProcessingTimeoutInSeconds=1800
RpcLocalPipeHost=127.0.0.1
ZoneIdentifierFiles=2
TimeoutResponse=4
StorageSyncIntervalInSeconds=15
```

The template the connector package is built from, with every optional key at its default. It declares no storage units: the synchronisation adds them once storages with event-based real-time protection exist in MDSS. When you download the connector from MDSS, MDSS fills in `Apikey`, `Port` and `PortSsl`, adds a `[Storage Unit 1]` section for the storage the connector was downloaded for, and sets `StorageUnits=1`.

```ini
[MetaDefender Storage Security]
IP=127.0.0.1
Port=80
PortSsl=443
IgnoreCertErrors=0
Apikey=
StorageUnits=0

[Settings]
LogRetentionCountInFiles=7
LogMaxFileSizeInMegabytes=10
LogPath=
LogLevel=Information
FileProcessingTimeoutInSeconds=3600
RpcLocalPipeHost=127.0.0.1
ZoneIdentifierFiles=0
TimeoutResponse=4
StorageSyncIntervalInSeconds=15
```

---

## Validation and troubleshooting

### What the connector logs at startup

After parsing succeeds, the connector dumps the effective configuration at `Information` level — the resolved values, with defaults already applied. One line is written per section, plus one per storage unit:

```plaintext
MetaDefender Storage Security <IP: 10.0.0.15. Port: 8008. PortSsl: 8443. IgnoreCertErrors: 1. Apikey: …>
Settings <LogRetentionCountInFiles: 14. LogMaxFileSizeInMegabytes: 50. LogPath: D:\mdss-connector-logs. LogLevel: Debug. FileProcessingTimeoutInSeconds: 1800. RpcLocalPipeHost: 127.0.0.1. ZoneIdentifierFiles: 2. TimeoutResponse: 4. StorageSyncIntervalInSeconds: 15>
Storage Unit <ClientId: 6f1c2f7a-…. SharePath: svm1\finance_share>
```

This is the fastest way to confirm the connector is reading the file you think it is, and that your edits took effect. An unrecognised or misspelled `[Settings]` key does not appear here; the default it failed to override does. A value that fell back to its default also shows the default here, next to the warning that explains why.

### Error messages and their causes

These stop the connector from starting:

| Log message | Cause |
| ---- | ---- |
| `Failed to read from .ini file. Section: …. Key: …` | Names the required key that is absent or empty (`IP`, `Port`, `Apikey`, `StorageUnits`, `ClientId`, `SharePath`), or the `[Storage Unit N]` section that does not exist |
| `Failed to read from .ini file at location …` | Summary line after the line above, or the file is missing from the executable's folder, or `StorageUnits` is not a valid count |
| `Invalid format for key IP` | `IP` is a hostname or not a valid IPv4 address |
| `Invalid value (must be integer). Key: Port` | `Port` contains a non-numeric value |
| `Value not in range [1,65535] for key Port` | `Port` is not a valid TCP port |
| `Invalid value for key (integer expected). Key: StorageUnits` | `StorageUnits` contains a non-numeric value |
| `Value must not be negative. Key: StorageUnits` | `StorageUnits` is negative |
| `Invalid key for storage unit. Key: …` | A `[Storage Unit N]` section contains a key other than `ClientId` or `SharePath` |
| `Invalid configuration inside config.ini file` | Summary line written after an `IP`, `Port` or `[Storage Unit N]` error |
| `Error when reading config.ini file` | Final line written at `Fatal` level after any of the above; the service does not start |

These do not stop the connector:

| Log message | Cause |
| ---- | ---- |
| `Invalid value (must be an integer) for key …. … Using the default: …` | A `[Settings]` key, `PortSsl` or `IgnoreCertErrors` contains a non-numeric value. The default is used |
| `Value out of range for key …. … Using the default: …` | A `[Settings]` key, `PortSsl` or `IgnoreCertErrors` is outside its range. The default is used. For retention, the message names `LogRetentionCountInDays` when the legacy key was the one read |
| `Invalid LogLevel value: …` | Misspelled or wrongly-cased log level. `Information` is used |
| `Configured LogPath cannot be used, logging to … instead. Configured path: …` | `LogPath` points to a directory that does not exist and cannot be created, or that the service account cannot write to. Logs go to the default directory |
| `Configured LogPath is relative, resolved against the installation directory: …` | Informational. Shows where a relative `LogPath` points |
| `Storage synchronisation is disabled (StorageSyncIntervalInSeconds=0)` | Informational. The synchronisation was turned off on purpose |
| `StorageSyncMonitor: could not enumerate storages from MDSS, skipping this cycle` | MDSS is unreachable, refused the request (for example, the API key has no read permission on accounts), or returned an unusable answer. Nothing is added or removed in this cycle |
| `Failed to find a MDSS storage unit for file …` | No `SharePath` matches the path ONTAP submitted |

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
