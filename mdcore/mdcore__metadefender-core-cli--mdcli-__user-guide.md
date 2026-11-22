<!-- source: https://www.opswat.com/docs/mdcore/metadefender-core-cli--mdcli-/user-guide -->

# MDCLI User Guide

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

`mdcli` is a cross-platform command-line client for **MetaDefender Core (MD Core)**. It submits one file, or streams a list of up to millions of file paths, to MD Core's REST API and emits the analysis results as JSON — designed to be embedded in CI/CD pipelines, kiosks/airgap transfer stations, and high-volume batch jobs.

- Results go to **stdout**; progress and errors go to **stderr**.
- The batch mode emits **NDJSON** (one JSON object per line), streamed as each file completes, with **O(1) memory** regardless of list size.
- A deterministic **exit-code contract** makes it scriptable.

`mdcli` is provided by OPSWAT as a **free utility** for MetaDefender Core customers. Version 1.0.0 is **validated with MetaDefender Core 5.20.0 and later versions.** See the [release notes](/docs/mdcore/metadefender-core-cli--mdcli-/release-notes) for what is in each version.

---

## [1. System requirements](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#1-system-requirements)

`mdcli` ships as a **single, statically-linked native binary** (built with `CGO_ENABLED=0`). It contains no interpreter and links no external shared libraries, so there is nothing to install alongside it.

### [Windows](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#windows)

| Item | Requirement |
| --- | --- |
| OS | Windows 10 / 11, or Windows Server 2016 or later |
| Architecture | x64 (amd64) |
| Runtime | None. No .NET, no Visual C++ redistributable |
| Privileges | Standard user (no administrator rights required) |
| Certificate store | Uses the built-in Windows certificate store for HTTPS |

### [Linux](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#linux)

| Item | Requirement |
| --- | --- |
| Distributions (validated) | SUSE Linux Enterprise 15+, Red Hat Enterprise Linux 8+ |
| Distributions (general) | Any Linux with kernel 3.2 or newer (Debian/Ubuntu, Rocky/Alma, Amazon Linux, etc.) |
| Architecture | x86-64 (amd64) and ARM64 (aarch64) |
| C library | **None required.** The binary is fully static — no glibc/musl dependency (`ldd ./mdcli` reports "not a dynamic executable") |
| Privileges | Standard user; must have read access to the files being scanned |
| CA certificates | For HTTPS to MD Core with certificate verification, the system CA bundle (`ca-certificates`) should be installed (see §2) |

Note

Because there is no libc dependency, a binary built once runs unchanged across SUSE 15, RHEL 8, and newer distributions — the classic "built on a newer distro, won't run on an older one" glibc problem does not apply.

---

## [2. Dependencies](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#2-dependencies)

**Runtime dependencies of the binary: none.** It is self-contained.

The only external things `mdcli` needs are environmental, not packages:

1. **Network reachability to MD Core's REST API** — by default `http://localhost:8008`. Ensure the host/port is reachable and any firewall permits it.
2. **CA certificates, only when using HTTPS with verification.**

   - **Windows:** handled automatically by the OS certificate store — nothing to do.
   - **Linux:** install the distro CA bundle so Go can verify the server certificate:

     - RHEL/Rocky/Alma: `sudo dnf install ca-certificates`
     - SUSE: `sudo zypper install ca-certificates`
     - Debian/Ubuntu: `sudo apt-get install ca-certificates`
   - Plain `http://` (e.g., a co-located Core on localhost) needs no certificates.
   - For a private/self-signed CA, either add the CA to the system trust store, or (dev/test only) pass `--tls-skip-verify`.
3. **Read access** to every file path you submit. `mdcli` streams file contents to Core; it does not copy files elsewhere or require temp space.

---

## [3. Installation](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#3-installation)

`mdcli` is distributed as a prebuilt binary — there is nothing to compile.

Release binaries are version-stamped (e.g. `1.0.0`) so releases are easy to tell apart.

1. Download the appropriate binary from [My OPSWAT](https://my.opswat.com) and copy it to the target host:

   - Linux x64: `mdcli-1.0.0-linux-amd64`
   - Linux ARM64: `mdcli-1.0.0-linux-arm64`
   - Windows x64: `mdcli-1.0.0-windows-amd64.exe`
2. **Linux** — place it on the `PATH` and make it executable:

   sudo install -m 0755 mdcli-1.0.0-linux-amd64 /usr/local/bin/mdcli
   mdcli --version # -> mdcli 1.0.0
3. **Windows** — copy `mdcli-1.0.0-windows-amd64.exe` to a folder (e.g. `C:\Program Files\mdcli\`), optionally rename to `mdcli.exe`, and add that folder to `PATH`:

   mdcli.exe --version # -> mdcli 1.0.0

Note

**Upgrading:** always confirm `mdcli --version` reports the expected number after installing, and check `command -v mdcli` (Linux) in case an older copy earlier in `PATH` is shadowing the new one.

---

## [4. Quick start](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#4-quick-start)

# 1. Point at your Core (env vars keep the API key out of shell history).
export MDCORE_URL="http://localhost:8008"
export MDCORE_APIKEY="<your-api-key>"
# 2. Scan a single file -> one indented JSON object on stdout.
mdcli --file ./installer.msi
# 3. Scan a list of paths -> NDJSON, one result per line, streamed live.
mdcli --from-file ./paths.txt > results.ndjson
# 4. Feed paths from another command via stdin.
find /data/incoming -type f | mdcli --from-file -

---

## [5. Command reference](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#5-command-reference)

mdcli [options] (exactly one of --file, --from-file or --directory is required)
### [Input / output](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#input--output)

| Option | Description |
| --- | --- |
| `--file <path>` | Scan a single file. Emits one indented JSON object. |
| `--from-file <path>` | Scan every newline-separated entry in the file. `-` reads the list from stdin. Emits NDJSON. Each entry is either a local file path or an `http(s)://` download URL (see below); the two may be mixed. |
| `--directory <root>` | Recursively scan regular local files beneath this root, including hidden files. Emits NDJSON. |
| `-o, --output <path>` | Write results to a file instead of stdout (`-` = stdout). |
| `--unscannable-as-skipped` | Report files Core could not examine (encrypted/password-protected, failed-to-scan, timeout, not-scanned) in the skipped report instead of counting them as detections. **Off by default.** |
| `--output-blocked` | Emit results only for files with a `Blocked` verdict (`MDCORE_OUTPUT_BLOCKED`). The run summary on stderr still counts every file. |
| `--version` | Print version and exit. |

Note

`--output-blocked` filters the JSON that reaches stdout; it's independent of `--fail-on` (which sets the exit code). A Blocked result carries the full AV/Deep CDR/sandbox detail under `result` for the client to inspect. Files that aren't Blocked — including non-Blocked errors — are simply not emitted.

### [Recursive directory scanning](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#recursive-directory-scanning)

mdcli --directory /data/incoming --run-dir /var/tmp/mdcli-runs/{runid}
mdcli --directory /data/incoming --batch-name backup-scan --no-hash-lookup

On Windows, use a quoted path such as `--directory "C:\Backup Files"`. The directory is on the machine running mdcli; files are uploaded to the Core selected by `--url`. Discovery streams through the existing bounded worker pool, without building a complete path list. Results arrive in completion order and use absolute local paths in `cli.input_path`. Core receives the complete path relative to the scan root: scanning `D:\backup\Users\Alice\report.txt` with `--directory D:\backup` reports `Users\Alice\report.txt` in Core history. The backup container is omitted automatically; no stripping or reporting-prefix option is needed. Directory separators follow the scan host's path syntax. Spaces, `#`, and (on Linux) newlines in filenames are preserved. Hidden files and subdirectories are included.

Submitted filenames are URL-encoded so Core retains directory components, spaces, and literal percent signs. CR/LF characters are removed from the name sent to Core; the original path remains in `cli.input_path`. Hash-cache hits reuse an existing Core record and do not create a new history entry with a new name; use `--no-hash-lookup` when each path must be recorded by Core.

Symbolic links inside the tree and special files (such as sockets and named pipes) are excluded; links are not followed. A root supplied through a symlink is resolved first. Zero-byte files use the existing skipped-file behavior. An empty directory completes successfully with no result records. Discovery is not a filesystem snapshot: avoid modifying the tree during a scan.

`--directory` cannot be combined with `--file`, `--from-file`, or `--prefix` (including a prefix inherited from configuration or the environment). Like the other input selectors, it is command-line only. Existing concurrency, hash lookup, detection, filtering, reporting, and batch options apply. Use `--no-hash-lookup` when every nonempty file must be uploaded into a Core batch.

Keep all output artifacts outside the input tree. Paths supplied through mdcli options are checked before files are created, including with `--force`; shell redirection is outside mdcli's control. An invalid/unreadable root exits 2 before any Core request. A later directory traversal error stops discovery, completes in-flight work and batch cleanup, and exits 5 with an error on stderr. Individual file read errors retain the usual per-file error reporting and exit behavior.

**Comments and blank lines.** In a list file, blank lines and comment lines are ignored. A line is a comment when its first character is `#` **followed by a space**, or when the line is only `#`. A `#` that is not followed by a space is treated as part of the path, since filenames may contain `#` — so `#tag.txt` and `## draft.bin` are paths, while `# note` and a lone `#` are comments.

# nightly set — updated 2026-07-30
/data/incoming/report.pdf
#archived.bin <- NOT a comment: a file literally named "#archived.bin"
# /data/skip-me.bin <- a comment (disabled entry)

**Download URLs in the list.** Any entry beginning with `http://` or `https://` is handed to Core via the `downloadfrom` header — Core fetches and scans it itself, so nothing is stored on the client. Such entries skip the local hash lookup (there are no local bytes to hash) and are reported with `source: download`. A single list may freely mix local paths and URLs. This is convenient for testing malware/early-termination handling (e.g. the EICAR test file) without writing a malicious file to local disk:

/data/incoming/report.pdf
https://secure.eicar.org/eicar.com.txt
/data/incoming/installer.msi

**Path prefix (--prefix).** When the paths in your list are *logical* source paths (e.g. from a backup catalog) but the files are actually reachable under a different mount on the scan host, `--prefix` bridges the two. It is prepended to each entry **only to read the file locally**; the original path is what appears in `cli.input_path` and is sent to Core as the filename (so Console reports and your catalog match). Example — catalog path `/foo/bar`, NFS mount `/mnt/malware/3`:

mdcli --from-file catalog.txt --prefix /mnt/malware/3
# list entry: /foo/bar
# file read: /mnt/malware/3/foo/bar
# reported as: /foo/bar (cli.input_path and Core display_name)

`--prefix` does not apply to `http(s)://` download-URL entries.

### [Files already accessible to Core](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#files-already-accessible-to-core)

Use `--core-local` to ask Core to read a file from its own filesystem instead of uploading its contents. Supply an absolute path as seen by Core:

mdcli --file /srv/backup/report.pdf --core-local
mdcli --from-file core-paths.txt --core-local --batch-name backup-job
mdcli --directory /srv/backup --core-local --batch-name backup-job

The selected Core workflow must enable **Allow scan files on server**, allow the supplied directory, and have permission to read the files. A shared drive accessible to Core also works. Windows drive paths and UNC file paths are accepted even when the CLI runs on Linux; POSIX absolute paths are accepted when the CLI runs on Windows. Relative Core paths and download URLs are rejected.

For `--file` and `--from-file`, mdcli neither opens nor stats the target file: Core checks its existence, readability, size, and scan eligibility. The list file itself is still read by mdcli. Empty server files are handled by Core rather than the CLI's local zero-byte skip. Per-file byte timings are zero because the CLI does not inspect the file; Core's result contains its file size when available.

For `--directory`, mdcli must be able to enumerate the tree locally, and the resulting absolute paths must refer to the same files on Core. This works when both run on the same host or use an identical shared mount. Core history names remain relative to the directory root. For different mount paths, supply a list of Core-visible absolute paths instead. With file/list input, `--prefix` is prepended before sending the Core path, using the CLI host's path-joining rules; it is not included in the reported name.

Core-local mode always disables client hashing and cache lookup, even when `--hash-lookup`, configuration, or environment settings enable it. It never falls back to uploading. Results keep `source: scan`; the JSON schema is unchanged. Core's own hashing and workflow behavior are unaffected.

### [Client hash lookup is opt-in](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#client-hash-lookup-is-opt-in)

By default mdcli submits files without calculating a client-side hash. Add `--hash-lookup` to calculate the selected `--hash-algo` and look up an existing Core result before uploading. Configuration `"hash_lookup": true` or environment `MDCORE_HASH_LOOKUP=true` also opts in, following the usual precedence rules. `--hash-algo` alone does not enable hashing.

Existing `--no-hash-lookup` remains a disabling compatibility flag; it cannot be combined with `--hash-lookup`. Even `--no-hash-lookup=false` does not opt in. `MDCORE_NO_HASH_LOOKUP=true` disables lookup if both old and new environment variables are set. With a config file active, those environment variables are ignored. Use `--hash-lookup=false` to override an opt-in config or environment.

### [Connection / authentication flags](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#connection--authentication-flags)

| Option | Env var | Default | Description |
| --- | --- | --- | --- |
| `--url` | `MDCORE_URL` | `http://localhost:8008` | MD Core base URL (http or https) |
| `--apikey` | `MDCORE_APIKEY` | — | API key. Prefer the env var (see §11) |
| `--rule` | `MDCORE_RULE` | — | MD Core workflow/rule to scan with |
| `--tls-skip-verify` | `MDCORE_TLS_SKIP_VERIFY` | `false` | Disable TLS certificate verification (dev/test only) |
| `--client-timeout` | `MDCORE_CLIENT_TIMEOUT` | `120s` | Per-HTTP-request timeout |

### [Scan behavior](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#scan-behavior)

| Option | Env var | Default | Description |
| --- | --- | --- | --- |
| `-j, --concurrency` | `MDCORE_CONCURRENCY` | `8` | Max files in flight at once (primary throughput/flow-control lever) |
| `--poll-interval` | `MDCORE_POLL_INTERVAL` | `500ms` | How often to poll each in-progress result |
| `--max-poll-wait` | `MDCORE_MAX_POLL_WAIT` | `10m` | Max time to wait for a single file's result before erroring it |
| `--no-hash-lookup` | `MDCORE_NO_HASH_LOOKUP` | `false` | Skip the pre-scan hash lookup; always upload |
| `--hash-lookup` | `MDCORE_HASH_LOOKUP` | `false` | Opt in to client hashing and pre-scan cache lookup; ignored in Core-local mode |
| `--core-local` | `MDCORE_CORE_LOCAL` | `false` | Submit a Core-visible absolute path with no upload or client hash; JSON config key `core_local` |
| `--hash-algo` | `MDCORE_HASH_ALGO` | `sha256` | Hash used for lookup: `md5|sha1|sha256|sha512` |
| `--retries` | `MDCORE_RETRIES` | `5` | Retries per request on transient failures (network error, 5xx, 503 queue-full) |
| `--prefix` | `MDCORE_PREFIX` | — | Path prepended to each input path **only when reading locally**; output and Core reporting keep the original path |

### [Run control](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#run-control)

| Option | Env var | Default | Description |
| --- | --- | --- | --- |
| `--fail-on` | `MDCORE_FAIL_ON` | `blocked` | What counts as a detection: `blocked|infected|suspicious|never` |
| `--stop-on-detection` | `MDCORE_STOP_ON_DETECTION` | `false` | Abort the whole run on the first detection (per `--fail-on`) |
| `--batch` | `MDCORE_BATCH` | `false` | Group a `--from-file` or `--directory` run into one MD Core batch (list and directory modes) |
| `--batch-name` | `MDCORE_BATCH_NAME` | — | Batch name, sent as MD Core batch `user_data` (implies `--batch`) |

Durations accept Go duration syntax: `500ms`, `30s`, `5m`, `1h30m`.

### [Monitoring a batch (`batch-status` subcommand)](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#monitoring-a-batch-batch-status-subcommand)

A read-only subcommand to check a batch's progress by id — safe to run from a separate, concurrent process while the scan is still going:

mdcli batch-status <batch_id> [--watch] [--json] [--watch-interval 2s]

| Flag | Default | Description |
| --- | --- | --- |
| `--watch` | `false` | Refresh until the batch is closed and all files have finished |
| `--watch-interval` | `2s` | Refresh cadence for `--watch` |
| `--json` | `false` | Emit one JSON object per refresh instead of a human line |
| (connection flags) |  | `--url`, `--apikey`, `--tls-skip-verify`, `--client-timeout` as above |

Human output:

batch 4725a285… finished 12 / 15 submitted result=Processing [open]

`[open]` vs `[closed]` reflects Core's `is_closed` (whether more files may still be submitted); `finished / submitted` is files completed over files added so far. See §9 for how to obtain the `batch_id` and the note on the denominator.

---

## [6. Configuration & precedence](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#6-configuration--precedence)

Settings can come from a **config file**, an **environment variable**, or a **command-line flag**.

### [6.1 Config file](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#61-config-file)

A JSON file holding the settings you want to reuse from run to run. Everything except *input selection* (`--file`/`--from-file`/`--directory`) and *command intent* (scan vs `batch-status`) can live in it — those stay on the command line.

| Option | Description |
| --- | --- |
| `--config <path>` | Load this file **and disable auto-discovery** |
| `--no-config` | Ignore any auto-discovered file; use flags/env only |
| `--print-config` | Print the effective configuration (API key redacted) and exit |

{
"url": "https://mdcore.internal:8008",
"apikey_env": "MDCORE_APIKEY",
"concurrency": 24,
"retries": 5,
"client_timeout": "120s",
"fail_on": "infected",
"prefix": "/mnt/malware/3",
"run_dir": "/var/lib/mdcli/runs/{runid}",
"log_level": "info"
}

Keys mirror the flag names with underscores (`client_timeout`, `hash_algo`, `stop_on_detection`, `output_blocked`, `skipped_file`, `stats_file`, `timing_file`, `log_file`, `log_dir`, `log_level`, `log_facility`, `log_success_limit`, `run_id`, `run_dir`, `manifest`, `force`). Durations are strings (`"120s"`). **Unknown keys are rejected**, so a typo fails loudly instead of being silently ignored.

### [6.2 Ignition file (auto-discovery)](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#62-ignition-file-auto-discovery)

If `--config` is not given, mdcli looks for a file named **mdcli.conf** and uses the **first** one it finds — files are never merged:

| Order | Location | Linux | Windows |
| --- | --- | --- | --- |
| 1 | working directory | `./mdcli.conf` | `.\mdcli.conf` |
| 2 | next to the binary | `<exe dir>/mdcli.conf` | `<exe dir>\mdcli.conf` |
| 3 | user config directory | `~/.config/mdcli/mdcli.conf` | `%APPDATA%\mdcli\mdcli.conf` |

`--config` overrides discovery; `--no-config` disables it. `--print-config` reports which file was actually loaded in its `config_source` field.

### [6.3 Precedence](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#63-precedence)

1. **Command-line flag** — always wins.
2. **Config file** (explicit or auto-discovered), if one is active.
3. **Environment variable** — *only when no config file is active*.
4. **Built-in default.**

Note

**Environment variables and config files do not mix.** Once a config file is in play, ambient `MDCORE_*` variables are ignored, so a configured run is fully determined by the file plus the command line — no surprises from a stray variable in the service environment. The one exception is explicit opt-in:

{ "apikey_env": "MDCORE_APIKEY" }

That tells mdcli to read the API key from the named variable, so the secret never has to be stored in the file. (mdcli errors out if the variable is unset.) With no config file at all, `MDCORE_*` behaves exactly as it always has.

The `MDCORE_*` variables describe the **MD Core server** the CLI connects to (its URL, key, rule, timeouts) — not the CLI itself.

mdcli --config /etc/mdcli/nightly.conf --print-config # dry-run: what will be used, and where output lands

---

## [7. Output format](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#7-output-format)

Each result is a JSON object with two parts — an additive `cli` envelope and the **verbatim, lossless** MD Core `AnalysisResult`:

{
"cli": {
"input_path": "/data/incoming/installer.msi",
"source": "scan",
"verdict": "Allowed",
"scan_result": "No Threat Detected",
"data_id": "…",
"hash": "…",
"hash_algo": "sha256"
},
"result": { "...": "full MD Core AnalysisResult, unmodified" }
}

- `source`: `scan` (uploaded), `hash-cache` (resolved via hash lookup, no upload), or `download` (Core fetched it from an `http(s)://` URL via `downloadfrom`).
- `verdict`: MD Core `process_info.result` — `Allowed`, `Blocked`, …
- On a per-file failure the object has `cli.error` set and omits `result`.

**Single-file mode** (`--file`) prints one indented object. **Multi-file mode** (`--from-file` or `--directory`) prints **NDJSON**: one compact object per line, flushed as each file finishes, so downstream tools can consume results live. Results arrive **out of order** (concurrency) — always key off `cli.input_path` or `cli.data_id`, never line position.

Consume with `jq` (one object per line):

mdcli --from-file paths.txt | jq -r 'select(.cli.verdict=="Blocked") | .cli.input_path'

---

## [8. Exit codes](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#8-exit-codes)

| Code | Meaning |
| --- | --- |
| `0` | Completed; nothing tripped `--fail-on` |
| `1` | Completed; ≥1 file tripped `--fail-on` (a detection) |
| `2` | Usage / argument error |
| `3` | Authentication or connection failure |
| `4` | Completed, but ≥1 file errored (e.g. upload/poll failure) |
| `5` | Internal CLI error |

Detection is **decided by MD Core and parsed by the CLI** from `process_info.result` and `scan_results.scan_all_result_i`; see §14.

### [Transient failures & retries](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#transient-failures--retries)

Every request to Core (hash lookup, submit, poll) is retried on **transient** failures — network errors (including Core temporarily unreachable), any HTTP **5xx**, and **503** (queue full) — up to `--retries` times (default 5) with jittered exponential backoff (250 ms, doubling to a 10 s cap; 503 honors Core's `Retry-After`). Auth failures (401/403), 4xx, and local errors (missing file) are **not** retried.

If retries are exhausted, the last error is recorded on that file and the run continues to the next one (per-file failures never abort a batch). The failed file appears in the output with `cli.error` set (and no `result`), and it maps to an exit code:

- a **connection/network** failure or auth rejection → exit **3**;
- any other per-file error (e.g. a 5xx that kept failing, a per-file `--max-poll-wait` timeout) → counts toward exit **4** (completed with errors).

Note `--client-timeout` bounds each individual HTTP attempt, and `--max-poll-wait` bounds total time waiting for one file's result; a truly unreachable Core will therefore fail a file in roughly `retries × client-timeout` at worst — tune both for your environment.

### [Error reference](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#error-reference)

Per-file failures appear in the JSON as `cli.error` (with no `result` block) and are also echoed to stderr as `error: <input_path> - <message>`. Messages are stage-prefixed so clients can branch on them. **Local I/O is checked up front, so an unreadable file fails immediately — before any upload — and is never retried.**

| `cli.error` | Cause | Retried? | Exit |
| --- | --- | --- | --- |
| `read: no such file or directory (<path>)` | Path missing, or broken symlink; with `--prefix` the *resolved* path is shown | no | 4 |
| `read: permission denied (<path>)` | File not readable by the mdcli user | no | 4 |
| `read: is a directory, not a file` | Entry points at a directory | no | 4 |
| `hash lookup: …` | Hash query to Core failed | transient only | 3 / 4 |
| `submit: …` / `submit url: …` | Upload or `downloadfrom` failed | transient only | 3 / 4 |
| `submit: authentication failed (HTTP 400|401|403): …` | Bad/missing API key | no | 3 |
| `poll: …` | Result retrieval failed | transient only | 3 / 4 |
| `poll: timed out waiting for scan to complete` | Exceeded `--max-poll-wait` | no | 4 |

Run-level failures (no JSON emitted) go to stderr only:

| stderr message | Exit |
| --- | --- |
| `error: cannot open --from-file: …` | 2 |
| `error: one of --file, --from-file or --directory is required` | 2 |
| `error: invalid --hash-algo "…" (want md5|sha1|sha256|sha512)` | 2 |
| `error: --file, --from-file and --directory are mutually exclusive` | 2 |

**Files Core cannot examine.** A password-protected/encrypted archive is returned by Core as `Blocked` with `scan_result: "Encrypted Archive"` (`scan_all_result_i` 12) — *not* as Infected, and with no engine detection. By default that still counts as a detection, because an encrypted archive is a recognised malware-delivery vector and suppressing it would weaken an existing gate. Pass `--unscannable-as-skipped` to instead record such files in the skipped report (reasons `encrypted`, `failed-to-scan`, `not-scanned`, `scan-timeout`) and keep them out of `--output-blocked`. A genuine Infected or Suspicious result is never re-routed. Extra `scan_all_result_i` values can be added via the `unscannable_codes` config key.

Notes:

- **Zero-byte files are skipped, not errors.** An empty file has no content to analyse, so mdcli skips it silently: nothing is uploaded, **no JSON record is emitted**, and it does not affect the exit code. Skipped entries are reported only as a count in the stderr summary (`… , N skipped`), so coverage still reconciles against the input list.
- **A bad file never aborts the run.** In list mode, mdcli reports the failure and continues; the stderr summary (`done: N scanned, N detected, N errored, N skipped`) gives the totals, and the process exits 4 if anything errored.
- **A failed download URL is reported by Core, not as a client error:** the record comes back `verdict: Blocked`, `scan_result: Failed`, with `result.download_info.status = "Download Failed"`. Under the default `--fail-on blocked` that counts as a detection (exit 1); use `--fail-on infected` if only real threats should gate the exit code.

---

## [9. Running large volumes in production](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#9-running-large-volumes-in-production)

`mdcli` is built for lists up to ~1,000,000 paths. The design keeps memory flat: the input list is read lazily line-by-line, files are streamed (never buffered whole), and results are written and flushed one at a time.

### [9.0 Run artifacts (unattended callers)](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#90-run-artifacts-unattended-callers)

A single scan can produce several output files. Rather than hard-coding a path for each — which a reused config would overwrite, and concurrent runs would corrupt — give the run an identity and let `mdcli` place the artifacts:

mdcli --from-file list.txt --run-dir /var/lib/mdcli/runs/{runid} --run-id job-12345/var/lib/mdcli/runs/job-12345/
├── results.ndjson scan results
├── skipped.ndjson entries with no verdict (errors + skips)
├── stats.json end-of-run summary
├── timings.ndjson per-file timings (only with --timing-file)
├── mdcli.log diagnostics (only when logging is enabled)
└── manifest.json run record + absolute path of every artifact

**Determinism contract.** When you pass `--run-id`, you already know every path: it is `<run-dir>/<fixed name>`. A server process needs no callback and no parsing — it can open `…/job-12345/results.ndjson` directly. If you omit `--run-id`, `mdcli` generates `<UTC-timestamp>-<pid>` and prints it on **stderr** (`run: <id> dir: <path>`); stdout stays pure NDJSON.

| Option | Purpose |
| --- | --- |
| `--run-id <id>` | Run identity. Letters, digits, `.`, `_`, `-` only. Generated if omitted. |
| `--run-dir <path>` | Directory for this run's artifacts. Supports `{runid}` `{timestamp}` `{pid}` `{host}`. |
| `--manifest <path>` | Manifest location when not using a run directory. |
| `--force` | Overwrite existing artifacts instead of failing. |

Notes:

- **--run-dir sends results to results.ndjson instead of stdout.** Pass `--output -` if you want to keep piping to `jq`.
- **An explicit path always wins**: `--skipped-file /elsewhere/s.ndjson` overrides the run-dir default, so artifacts can live on different volumes.
- **Diagnostic artifacts stay opt-in.** A run directory does not silently enable per-file timings or the diagnostic log; those still require their own flag.
- **Collisions fail loudly.** A non-empty run directory, or an existing artifact, is a usage error (exit 2) — a new session can never silently destroy the previous one. Files are created with `O_EXCL`, which is atomic, so two concurrent runs cannot race onto the same path either.
- Placeholders also work in `--output`, `--skipped-file`, `--timing-file`, `--stats-file`, `--log-file` and `--log-dir` if you prefer a flat layout, and all of them expand with the *same* timestamp within a run.

**Manifest** (`status` is `running` until the run ends, then `completed` or `failed`; artifacts that were never written are pruned):

{"run_id":"job-12345","mdcli_version":"1.0.0","host":"scanhost","pid":4821,
"started_at":"2026-08-07T16:57:35Z","finished_at":"2026-08-07T17:41:10Z",
"status":"completed","exit_code":1,
"run_dir":"/var/lib/mdcli/runs/job-12345",
"artifacts":{"results":"…/results.ndjson","skipped":"…/skipped.ndjson",
"manifest":"…/manifest.json"},
"summary":{"scanned":812304,"detected":12,"errored":3,"skipped":940}}

Exit 4 (finished with per-file errors) still counts as `completed` — the run reached the end of its work. Only usage, auth/connection and internal failures (exit 2/3/5) are `failed`.

**Retention.** `mdcli` never deletes anything at runtime; each run is a self-contained directory, so cleanup is a maintenance job. Use age as the criterion and `status` as a guard against removing a run still in flight:

find /var/lib/mdcli/runs -mindepth 1 -maxdepth 1 -type d -mtime +14 -exec rm -rf {} +

Tip: `--print-config` reports the resolved artifact paths *before* any scanning starts — a cheap dry-run check for an unattended job.

### [9.0.2 Diagnostic log](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#902-diagnostic-log)

`mdcli` can write an operational log to a file, in **RFC 5424 syslog format** by default, so an existing pipeline (rsyslog `imfile`, Filebeat, Fluentd) can tail and forward it. The log is **independent of stderr**: stderr serves the interactive user or the calling process; the log file serves offline diagnostics.

| Option | Default | Description |
| --- | --- | --- |
| `--log-file <path>` | — | Explicit log path |
| `--log-dir <folder>` | — | Write `mdcli.log` in this folder (or the run dir) |
| `--log-level` | `info` | `debug|info|warn|error` |
| `--log-facility` | `local0` | Syslog facility |
| `--log-success-limit` | `100` | Log the first N clean scans individually, then one rollup per N (`0` = log all) |

<134>1 2026-08-07T19:56:24.551Z scanhost mdcli 295059 run-start [mdcli@0 run_id="job-L"] version=1.0.0 url=… concurrency=4 fail_on=blocked batch=false
<134>1 2026-08-07T19:56:25.357Z scanhost mdcli 295059 file-clean [mdcli@0 run_id="job-L"] path="/data/f1.txt" source=scan verdict=Allowed total_ms=804
<131>1 2026-08-07T19:56:26.783Z scanhost mdcli 295059 file-error [mdcli@0 run_id="job-L"] path="/data/gone.txt" reason=missing error="read: no such file or directory (…)"
<134>1 2026-08-07T19:56:26.783Z scanhost mdcli 295059 progress [mdcli@0 run_id="job-L"] 5 files processed cleanly, avg 718ms
<132>1 2026-08-07T19:56:28.887Z scanhost mdcli 295059 file-detected [mdcli@0 run_id="job-L"] path="…/eicar.com.txt" verdict=Blocked scan_result="Infected" data_id=c37b82e7… total_ms=2104
<134>1 2026-08-07T19:56:28.887Z scanhost mdcli 295059 run-summary [mdcli@0 run_id="job-L"] scanned=14 detected=1 errored=1 skipped=1 wall_ms=4335 files_per_sec=3.23

Event IDs (the RFC 5424 MSGID field) are stable and greppable: `run-start`, `run-summary`, `run-failed`, `batch-start`, `batch-close`, `batch-close-failed`, `file-clean`, `file-detected`, `file-error`, `file-skipped`, `progress`.

**Volume control.** Errors, detections, skips and the batch/run lifecycle are **always** logged. Only clean results are sampled: the first `--log-success-limit` are logged individually, and thereafter one `progress` line summarises each group of that many (a partial group is flushed at the end, so the counts always reconcile). At a million files with the default of 100 that is ~10,000 progress lines instead of a million.

**No rotation, no appending.** Each invocation writes a *new* file — mdcli is a CLI, not a daemon, so rotation is unnecessary. Re-using an existing log path is an error (exit 2); use `{runid}`/`{timestamp}` placeholders, `--log-dir` inside a per-run directory, or `--force`.

The `run_id` travels in every line's structured data, so forwarded lines stay correlatable with the run's other artifacts.

### [9.0.1 Performance measurement](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#901-performance-measurement)

Timings are **client-observed wall clock** — they include network and queue wait, which Core's own `processing_time` cannot show. Two independent outputs:

| Option | Cost | Content |
| --- | --- | --- |
| `--stats-file <path>` | one small object | End-of-run aggregate. Cheap enough for production. |
| `--timing-file <path>` | one line per file | Per-file phase breakdown. A tuning aid; leave off for production scans. |

A run summary is **always** produced: it goes to `--stats-file` as JSON when given, otherwise to stderr as three compact lines.

stats: 8 scanned (0 cache, 8 upload, 0 download), 0 detected, 0 errored, 1 skipped
stats: 3.6s wall, 2.20 files/s, 0.42 MB/s, 0 retries, concurrency 4
stats: latency p50 1300ms p90 1348ms p95 1348ms p99 1348ms max 1983ms

Per-file record (`--timing-file`):

{"input_path":"/data/f3.bin","data_id":"3fc795a6…","source":"scan","bytes":200000,
"submit_ms":1203,"wait_ms":724,"total_ms":1928,"started_at":"2026-08-07T18:29:52Z"}

`hash_ms` local hashing · `lookup_ms` hash-lookup round trip · `submit_ms` upload or `downloadfrom` · `wait_ms` submit→verdict · `total_ms` end-to-end · `retries` transient retries. Phases that did not occur are omitted, so a `hash-cache` hit shows no `submit_ms`/`wait_ms` — making the dedup saving directly visible. The aggregate's `sources` block does the same at run level.

Notes:

- **The result schema is unchanged.** Timings never appear in the results NDJSON, so existing consumers are unaffected whether or not you enable them.
- Durations are whole **milliseconds**; an operation faster than 1 ms reads `0`.
- Percentiles come from a fixed-bucket histogram, so memory is constant whether the run covers ten files or a million. Values carry two significant digits (≤10% overstatement) and are clamped to the observed maximum; `--timing-file` has the exact per-file numbers when you need them.

### [9.1 Recipe](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#91-recipe)

export MDCORE_URL="https://mdcore.internal:8008"
export MDCORE_APIKEY="…"
# Build the work list (or maintain it however you like).
find /data/to-scan -type f > /var/tmp/scan-list.txt
# Scan, tuned for your Core's capacity, capturing NDJSON + a log.
mdcli --from-file /var/tmp/scan-list.txt \
--concurrency 24 \
--fail-on infected \
--output /var/tmp/scan-results.ndjson \
2> /var/tmp/scan.log
echo "exit=$?" # 0 clean, 1 detection, 3 infra, 4 partial errors
### [9.2 Streaming from a generator (no intermediate list file)](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#92-streaming-from-a-generator-no-intermediate-list-file)

find /data/to-scan -type f | mdcli --from-file - -j 24 > results.ndjson
### [9.3 Consuming results while the run is in progress](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#93-consuming-results-while-the-run-is-in-progress)

Because NDJSON is flushed per file, you can tail and process live:

tail -f results.ndjson | jq -c '{path: .cli.input_path, verdict: .cli.verdict}'
### [9.4 Flow control against Core](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#94-flow-control-against-core)

- **Concurrency (-j) is the main lever.** It caps how many files are in flight.
- If Core's scan queue fills, it returns **HTTP 503**; `mdcli` automatically backs off per file — exponential backoff with full jitter, starting at 250 ms, doubling to a 10 s cap, up to 8 retries (honoring `Retry-After` when present). Workers block during backoff, which naturally reduces pressure.
- Start conservative (`-j 8`–`16`), watch throughput and the `errored` count, and raise gradually. Too high just produces more 503s and backoff, not more speed — the ceiling is Core's engine/queue capacity, not the client.

### [9.5 Batch mode](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#95-batch-mode)

With `--batch` (list and directory modes), `mdcli` opens a single MD Core **batch** before submitting the first file, associates every submission with it, and closes the batch when the run finishes — so the job is one logical unit on Core (for batch-level reporting/auditing). Each submitted file gets its own `data_id`; the batch groups them. (Files resolved by dedup aren't submitted — see below.)

mdcli --from-file /var/tmp/scan-list.txt \
--batch --batch-name "nightly-$(date +%F)" \
--output results.ndjson
# stderr: batch started: <batch_id> (name "nightly-2026-07-16")
# batch closed: <batch_id>
# done: N scanned, N detected, N errored, N skipped

- `--batch-name` is sent as the batch's `user_data` and implies `--batch`.
- The opened `batch_id` is announced on **stderr at the start** (`batch started: …`) and included in the output record of every **submitted** file (`cli.batch_id`). stdout stays pure JSON, so a downstream `jq` consumer is never confused by the id — capture it from stderr.
- **Dedup interacts with batches.** Hash lookup (dedup) still applies in batch mode: a cache hit is served from Core's hash store — its result is retrieved and reported (as `source: hash-cache`) — but it is **not re-submitted**, so it is not a member of the batch and carries no `batch_id`. In practice a real batch is rarely fully cached, so most files are submitted and appear in the batch. To force **every** file into the batch (e.g. a test where all inputs are already cached), add `--no-hash-lookup`.
- The batch is closed with a fresh 30 s timeout even if the run is cancelled (e.g. `--stop-on-detection`), so batches are not left open on Core.
- Without `--batch`, files are submitted independently (no batch) — the default.

**Monitoring progress concurrently.** Grab the `batch_id` from the start line on stderr and poll it from another process with the `batch-status` subcommand:

mdcli batch-status <batch_id> --watch --watch-interval 2s
# batch <id> finished 12 / 15 submitted result=Processing [open]
# batch <id> finished 15 / 15 submitted result=Allowed [closed]

Denominator note: a standalone monitor knows only what Core reports — **files finished over files added so far** — because the eventual total isn't fixed until every file is submitted (e.g. when the list itself is streamed). The count is firm once the batch shows `[closed]`.

### [9.6 Automation patterns](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#96-automation-patterns)

- **CI/pipeline gate:** run to completion, let the exit code fail the job (`--fail-on infected` to gate on real threats only; default `blocked` to gate on any Core block, including DLP/CDR/type policy).
- **Fast fail:** `--stop-on-detection` aborts the run on the first detection. Works with `--batch`: the batch is still closed on Core (best-effort, on a fresh timeout), and files that were in flight when the run aborted are dropped from the output rather than reported as errors — the client gets the first detection and stops. A few of those in-flight files may already have reached Core and remain in the batch there; that's expected and bounded by concurrency (and Core's queue).
- **Report-only:** `--fail-on never` always exits 0 (still emits full results) so a reporting job never fails the pipeline.

---

## [10. Performance & tuning](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#10-performance--tuning)

| Concern | Behavior / guidance |
| --- | --- |
| Memory | O(1) in list size. Roughly `concurrency × (response size + buffers)`. Per-response body is capped at 64 MB. |
| CPU | Low; the workload is network- and Core-bound. Local hashing (for the lookup) reads each file once. |
| Upload | File bodies are streamed, not buffered — large files do not inflate memory. |
| Hash lookup | Off by default. Opt in with `--hash-lookup` to calculate a client hash and reuse existing Core results. Core-local mode never hashes on the client. |
| In-progress hits | If a hash lookup finds an analysis still running, `mdcli` polls that existing analysis rather than re-uploading. |
| `--client-timeout` | Raise for very large uploads over slow links. |
| `--max-poll-wait` | Raise if Core legitimately takes long (large archives, deep CDR); lower to fail slow files faster. |
| File descriptors (Linux) | High `-j` opens more sockets/files at once. Ensure `ulimit -n` is adequate (e.g. `ulimit -n 4096`). |

---

## [11. Security](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#11-security)

- **API key:** prefer `MDCORE_APIKEY` over `--apikey`. A flag value is visible in shell history and in process listings (`ps`, Task Manager); the env var is not. The key is never written to stdout/stderr by `mdcli`.
- **TLS:** verification is **on by default**. `--tls-skip-verify` disables it and should be limited to development/testing — it exposes the connection to MITM.
- **Least privilege:** `mdcli` only needs a scan-scoped API key and read access to the target files. It uses no administrative MD Core endpoints.
- **Untrusted content:** the CLI streams bytes to Core and never executes or parses file contents locally, keeping local attack surface minimal.

---

## [12. Troubleshooting](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#12-troubleshooting)

| Symptom | Likely cause / fix |
| --- | --- |
| Exit 3, "connection refused" | Wrong `--url`/port, Core down, or firewall. Verify `curl <url>/version`. |
| Exit 3, HTTP 401/403 | Bad or missing API key. Check `MDCORE_APIKEY`. |
| Exit 1 but no malware | A non-threat block (e.g. `Sanitization Timed Out`, DLP, blocked type). Use `--fail-on infected` to gate on threats only; inspect `result.process_info.blocked_reason`. |
| Many `errored`, HTTP 503 | Core queue saturated. Lower `-j`; backoff is already automatic. |
| Files stuck / slow | Core-side scanning slow (e.g. sandbox/CDR). Check Core module health; adjust `--max-poll-wait`. |
| TLS "certificate signed by unknown authority" (Linux) | Install `ca-certificates`, or add your private CA to the trust store. `--tls-skip-verify` for test only. |
| `too many open files` (Linux) | Raise `ulimit -n`, or lower `-j`. |
| Result shows `source: hash-cache` but you expected a fresh scan | Core returned a prior result for that hash. Use `--no-hash-lookup` to force re-upload. Note Core may flag stale results with `outdated_data`. |

`mdcli` writes diagnostics and a `done: N scanned, N detected, N errored, N skipped` summary to stderr; redirect it (`2> run.log`) to keep an audit trail.

---

## [13. Known limitations](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#13-known-limitations)

Current version. Planned items are on the project roadmap:

- **Operational conditions count as blocks.** With the default `--fail-on blocked`, Core results like *Sanitization Timed Out* or *Failed to Scan* trip exit 1 even though no threat was found. Use `--fail-on infected`/`suspicious` to gate on real verdicts. A dedicated result-code → exit-condition map is planned.
- **No resume/checkpoint.** An interrupted large run restarts from the beginning of the list (the hash cache makes re-runs cheap for already-known files).
- **No archive child/blocked-leaves reporting** yet (the full `result` still contains Core's data; there is no CLI-level per-leaf summary).
- **Output formats:** JSON/NDJSON only (no table/CSV yet).
- **Transport:** HTTP/2 is negotiated automatically over HTTPS; plaintext HTTP is HTTP/1.1 (h2c is not used).

---

## [14. Appendix: verdicts & result codes](/docs/mdcore/metadefender-core-cli--mdcli-/user-guide#14-appendix-verdicts--result-codes)

`--fail-on` decides what counts as a "detection" for the exit code and for `--stop-on-detection`:

| `--fail-on` | Trips when |
| --- | --- |
| `blocked` (default) | `process_info.result == "Blocked"` — any reason (malware, DLP, CDR, blocked type, timeouts) |
| `infected` | `scan_results.scan_all_result_i == 1` (Infected) — a real AV/threat detection |
| `suspicious` | `scan_all_result_i` is `1` (Infected) or `2` (Suspicious) |
| `never` | Nothing trips; always exit 0 (report-only) |

Key MD Core `scan_all_result_i` values you may see in `cli.scan_result` / `result.scan_results.scan_all_result_a`:

| Code | Meaning |
| --- | --- |
| 0 | No Threat Detected |
| 1 | Infected |
| 2 | Suspicious |
| 3 | Failed to Scan |
| 10 | Not Scanned / engine unavailable |
| … | Other codes exist (e.g. timeouts); the full `result` block preserves them verbatim |

Note

The result-code list above covers the common cases; MD Core defines additional codes. The complete, unmodified result is always available under `result` for downstream consumers.
