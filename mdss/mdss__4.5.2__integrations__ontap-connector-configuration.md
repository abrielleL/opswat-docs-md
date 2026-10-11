<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/ontap-connector-configuration -->

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
| Applying a change | **Restart the opswat-ontap-connector service.** The file is never re-read at runtime. |

`config.ini` is copied from the executable folder into the installation folder by `--install` and `--upgrade`, so edit the *installed* copy when tuning a deployed connector.

If the file cannot be read, or any value fails validation, the connector logs `Error when reading config.ini file` at `Fatal` level and exits without starting.

### Format rules

Standard INI semantics apply:

- Sections are declared as `[Section Name]`; section and key names are matched case-insensitively by Windows.
- Entries are `Key=Value`. Whitespace around the `=` is trimmed.
- Lines beginning with `;` are comments.
- Do **not** quote values — quotes become part of the value.
- A single value is limited to 254 characters; anything longer is truncated.

---

## Section `[MetaDefender Storage Security]`

Identifies the MDSS instance the connector talks to.

| Key | Required | Type | Default | Accepted values |
| ---- | ---- | ---- | ---- | ---- |
| `IP` | Yes | IPv4 address | — | Dotted-quad IPv4 only, e.g. `10.0.0.15` |
| `Port` | Yes | Integer | — | MDSS HTTP port, e.g. `80`, `8008` |
| `PortSsl` | No | Integer | `443` | MDSS HTTPS port |
| `IgnoreCertErrors` | No | Integer | `0` | `0` or `1` |
| `Apikey` | Yes | String | — | MDSS API key |
| `StorageUnits` | Yes | Integer | — | `1` or greater |

### `IP`

The address of the MDSS instance. **Validated against an IPv4 regular expression — hostnames. FQDNs and IPv6 addresses are rejected** and cause a fatal configuration error at startup.

### `Port` and `PortSsl`

The connector does not require you to declare whether MDSS is served over HTTP or HTTPS. It starts every session on plain HTTP against `Port`, and switches transport automatically:

1. A request fails with a transport-level WinHTTP error — TLS handshake failure (`12175`), connection reset (`12030`), an invalid server response (`12152`), or the port refusing connections (`12029`).
2. The connector flips its transport mode (HTTP ⟷ HTTPS) and retries the request once on the other port.
3. The new mode is kept for subsequent requests, and the switch is logged at `Warning` level (`MDSS request failed with a transport error. Switched transport to …`).

The switch is bidirectional and self-healing, so an MDSS instance that moves from HTTP to HTTPS (or back) is picked up without restarting the connector. Automatic switching is only attempted when `PortSsl` is greater than `0`; setting `PortSsl=0` pins the connector to plain HTTP on `Port`.

The connector negotiates TLS 1.2 and, where the build environment supports it, TLS 1.3.

### `IgnoreCertErrors`

| Value | Behaviour |
| ---- | ---- |
| `0` (default) | Full TLS certificate validation. A certificate MDSS cannot prove is trusted fails the request. |
| `1` | Certificate errors are ignored on HTTPS requests: unknown CA, wrong certificate usage, host-name mismatch, and expired/not-yet-valid dates. |

Set this to `1` when MDSS is serving its default self-signed certificate. Any other value (for example `2`) is a fatal configuration error. The setting has no effect on plain HTTP requests.

> Security note: `IgnoreCertErrors=1` disables certificate validation entirely and leaves the channel open to an on-path attacker. Use it only on trusted management networks, or install a certificate the connector's host trusts.

### `Apikey`

The MDSS API key, sent as the `Apikey` HTTP header on every call the connector makes (`POST /api/webhook/realtime`, `GET /api/file/{correlationId}`, `GET /api/health`).

This will be automatically added when you download and install the OPSWAT ONTAP Connector from MDSS.

### `StorageUnits`

The number of `[Storage Unit N]` sections that follow. Must be an integer of at least `1`; `0`, a negative number or a non-numeric value is a fatal configuration error.

The connector reads exactly the sections `[Storage Unit 1]` … `[Storage Unit <StorageUnits>]`. **Numbering must be consecutive and start at 1** — a gap causes the missing section's read to fail. Sections beyond the declared count are ignored.

---

## Section `[Storage Unit N]`

One section per storage unit, numbered `1` to `StorageUnits`. Both keys are required in every section.

| Key | Required | Type | Default | Description |
| ---- | ---- | ---- | ---- | ---- |
| `ClientId` | Yes | String | — | The MDSS storage client id |
| `SharePath` | Yes | String | — | ONTAP-side path prefix for this storage unit |

### `ClientId`

The client id of the storage configured in MDSS. It is sent as `storageClientId` in the real-time webhook payload and tells MDSS which storage the file belongs to. Copy it from the storage's configuration in MDSS.

### `SharePath`

The ONTAP path prefix that identifies files belonging to this storage unit, for example `svm1\share1`. The value is used twice on each incoming scan request:

1. **Storage-unit selection.** The connector takes the path ONTAP sent and finds the first storage unit whose `SharePath` appears in it. The match is a case-insensitive substring search. If no unit matches, the file is dropped with `Failed to find a MDSS storage unit for file …` at `Error` level and ONTAP never receives a verdict for it.
2. **Computing the MDSS-relative path.** ONTAP paths arrive as `\\?\UNC\<path>`. The connector strips the 8-character `\\?\UNC\` prefix, then strips `SharePath` plus one separator from the front of what remains. The result is the relative path sent to MDSS as the file's `name`.

Because step 2 removes a fixed number of characters, `SharePath` must be **the exact leading portion of the ONTAP path after \\?\UNC\** — not merely a substring that happens to appear somewhere in it. A value that is too short or too long produces a wrong relative path and MDSS will not find the file.

Leading backslashes are stripped when the value is read, so `\svm1\share1` and `svm1\share1` are equivalent. Do not add a trailing separator.

When several storage units are configured, order matters: the first match wins, so avoid share paths where one is a prefix of another, or list the most specific first.

---

## Section `[Settings]`

Every key in this section is optional. A missing or empty key falls back to its default; a present but invalid value is a fatal configuration error.

| Key | Type | Default | Range / accepted values |
| ---- | ---- | ---- | ---- |
| `LogRetentionCountInDays` | Integer | `7` | `1` – `30` |
| `LogLevel` | String | `Information` | `Verbose`, `Debug`, `Information`, `Warning`, `Error`, `Fatal` |
| `FileProcessingTimeoutInSeconds` | Integer | `3600` | Any integer |
| `RpcLocalPipeHost` | String | `127.0.0.1` | An address, or the literal `NULL` |
| `ZoneIdentifierFiles` | Integer | `0` | `0` – `3` |
| `TimeoutResponse` | Integer | `4` | `0` – `5` |

### `LogRetentionCountInDays`

How many log files to keep. The connector writes one file per day to a `logs` folder next to the executable, named `YYYYMMDD.log`. A rotation thread runs every 10 seconds; it rolls over to a new file when the date changes and deletes the oldest files until only `LogRetentionCountInDays` remain.

Values outside `1` – `30` are rejected with `Value not in range [1,30]`.

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

**The value is compared case-sensitively**, so it must be spelled exactly as listed — `information` is rejected with `Invalid LogLevel value …`.

Note that the level only takes effect once the service main thread starts; configuration parsing itself is logged at `Verbose`, which is why the startup banner and the configuration dump always appear.

When the executable is run interactively (`--install`, `--uninstall`, `--upgrade`) output goes to the console instead of a file. File logging is used for `--service` and `--debug`.

### `FileProcessingTimeoutInSeconds`

How long a single file may stay in the connector's pipeline, measured from the moment ONTAP's scan request was received. When the timeout is exceeded and MDSS has still not returned a final verdict — or the connector cannot reach MDSS or ONTAP at all — the connector gives up on the file: it sends the verdict configured in `TimeoutResponse` to ONTAP and removes the file from its tracking list. Exactly one timeout verdict is sent per file.

The default `3600` (one hour) is deliberately generous: it must accommodate the slowest case MDSS can produce, including large archives and Deep CDR. Lowering it makes the connector give up sooner on files MDSS is still working on. No range validation is applied to this key.

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

Values outside `0` – `3` are rejected with `Value not in range [0,3]`.

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

Values outside `0` – `5` are rejected with `Value not in range [0,5]`. Use `0` or `1` for availability-first deployments, `2` or `3` for security-first, and `5` when several scanners serve the same ONTAP cluster and another one should get a chance at the file.

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
SharePath=ONTAP_ADMIN$

[Storage Unit 2]
ClientId=9d4b8e01-11aa-42cc-8e77-5b6c9d0e2222
SharePath=ONTAP_ADMIN$

[Settings]
LogRetentionCountInDays=14
LogLevel=Debug
FileProcessingTimeoutInSeconds=1800
RpcLocalPipeHost=127.0.0.1
ZoneIdentifierFiles=2
TimeoutResponse=4
```

The shipped template, with every optional key at its default:

```ini
[MetaDefender Storage Security]
IP=127.0.0.1
Port=80
PortSsl=443
IgnoreCertErrors=0
Apikey=
StorageUnits=1

[Storage Unit 1]
ClientId=
SharePath=

[Settings]
LogRetentionCountInDays=7
LogLevel=Information
FileProcessingTimeoutInSeconds=3600
RpcLocalPipeHost=127.0.0.1
ZoneIdentifierFiles=0
TimeoutResponse=4
```

---

## Validation and troubleshooting

### What the connector logs at startup

After parsing succeeds, the connector dumps the effective configuration at `Information` level — the resolved values, with defaults already applied. Three lines are written, one per section:

```plaintext
MetaDefender Storage Security <IP: 10.0.0.15. Port: 8008. PortSsl: 8443. IgnoreCertErrors: 1. Apikey: …>
Settings <LogRetentionCountInDays: 14. LogLevel: Debug. FileProcessingTimeoutInSeconds: 1800. RpcLocalPipeHost: 127.0.0.1. ZoneIdentifierFiles: 2. TimeoutResponse: 4>
Storage Unit <ClientId: 6f1c2f7a-…. SharePath: svm1\finance_share>
```

This is the fastest way to confirm the connector is reading the file you think it is, and that your edits took effect.

### Error messages and their causes

| Log message | Cause |
| ---- | ---- |
| `Failed to read from .ini file at location …` | The file is missing from the executable's folder, or a required key is absent |
| `Invalid format for key IP` | `IP` is empty, a hostname, or not a valid IPv4 address |
| `Invalid value (must be integer). Key: …` | A numeric key contains a non-numeric value |
| `Invalid value (must be 0 or 1). Key: IgnoreCertErrors` | `IgnoreCertErrors` is set to something other than `0` or `1` |
| `Value must be greater than 0. Key: StorageUnits` | `StorageUnits` is `0` or negative |
| `Value not in range [1,30] for key LogRetentionCountInDays` | Retention outside the supported range |
| `Value not in range [0,3] for key ZoneIdentifierFiles` | Unsupported Zone.Identifier mode |
| `Value not in range [0,5] for key TimeoutResponse` | Unsupported timeout response mode |
| `Invalid LogLevel value '…'` | Misspelled or wrongly-cased log level |
| `Invalid configuration inside config.ini file` | Summary line written after any of the above; the service does not start |
| `Failed to find a MDSS storage unit for file …` | No `SharePath` matches the path ONTAP submitted |

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
