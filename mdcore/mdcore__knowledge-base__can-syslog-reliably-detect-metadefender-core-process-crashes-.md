<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes- -->

# Can Syslog Reliably Detect MetaDefender Core Process Crashes?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [Question](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#question)

Can “warning” or “error” **Syslog** messages be used as a reliable signal that critical MetaDefender Core processes (e.g., `ometascan.exe`, `engineprocess.exe`, `nginx.exe`, `postgres.exe`) have **crashed** or become **unresponsive**? If not, are there *any* crash events that appear in Syslog?

## [Short answer](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#short-answer)

**No. Do not rely on Syslog severity (warning/error) to detect process crashes or hangs.** A hard crash (e.g., OOM, SIGKILL, power loss) often prevents the application from emitting any Syslog line at all. Even when errors are logged, they’re not guaranteed to uniquely indicate a crash of a specific process.

Use **direct process/service monitoring** at the OS level and/or infrastructure health checks.

## [Why Syslog isn’t reliable for crash detection](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#why-syslog-isnt-reliable-for-crash-detection)

- **Crashes are abrupt.** On OOM/SIGKILL or sudden exits, the process cannot log a “we are crashing” message.
- **Severity isn’t specific.** “warning”/“error” messages can reflect transient conditions, timeouts, or engine-specific issues—not a confirmed crash.
- **Log pipeline can be affected.** If logging/forwarding is colocated, a crash or high load can drop/skip messages.

## [Recommended approach (process-level monitoring)](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#recommended-approach-process-level-monitoring)

### [Processes to monitor](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#processes-to-monitor)

- `ometascan.exe` – main MetaDefender Core process
- `engineprocess.exe` – engine worker processes (ClamAV may appear as `clamd.exe`)
- `nginx.exe` / `nginx` – web front end
- `postgres.exe` / `postgres` – database (when bundled)

### [Windows](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#windows)

- **Service/Process checks**

  - PowerShell (example

HtmlCopy$names = 'ometascan','engineprocess','nginx','postgres'
$down = $names | ForEach-Object {
if (-not (Get-Process -Name $_ -ErrorAction SilentlyContinue)) { $_ }
}
if ($down) { Write-Error "Missing processes: $($down -join ', ')" }

- - Configure **Service Recovery** (Services → Recovery tab) to restart on failure and run a script to alert.
- **Crash signals you** ***can*** **forward to Syslog**

  - Windows Event Log → *Application* / *System* (e.g., **Application Error** / **Service Control Manager** events).
  - Use an agent (e.g., NxLog/Winlogbeat) to forward these **OS-level** crash/stop events to your SIEM/Syslog.

### [Linux](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#linux)

- **Process checks**

  - `pgrep -x ometascan || echo "ometascan missing"`
  - `pgrep -x nginx || echo "nginx missing"`
  - `pgrep -x postgres || echo "postgres missing"`
- **systemd watchdog (if applicable)**

  - Use `systemctl is-active <unit>` and configure `Restart=on-failure`.
- **Crash signals you** ***can*** **forward to Syslog**

  - `journald` / `rsyslog` can send kernel/app crashes (e.g., `segfault`, OOM killer) to your SIEM.

> Tip: Also monitor **UI/API liveness** (TCP/HTTP) and **queue/backlog** metrics where available. A process might be up but unresponsive.

## [What Syslog is good for (and not)](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#what-syslog-is-good-for-and-not)

## [Minimal alerting examples](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#minimal-alerting-examples)

**Windows (scheduled every minute)**

HtmlCopy$must Have = 'ometascan','engineprocess','nginx','postgres'
$missing = $mustHave | Where-Object { -not (Get-Process -Name $_ -ErrorAction SilentlyContinue) }
if ($missing) {
# send to your alerting endpoint here
Write-Error "MetaDefender Core critical processes down: $($missing -join ', ')"
}

**Linux (cron every minute)**

HtmlCopymissing=()
for p in ometascan engineprocess nginx postgres; do
pgrep -x "$p" >/dev/null || missing+=("$p")
done
[ ${#missing[@]} -gt 0 ] && echo "Missing: ${missing[*]}" >&2
## [Conclusion](/docs/mdcore/knowledge-base/can-syslog-reliably-detect-metadefender-core-process-crashes-#conclusion)

- **Do not** treat Syslog warning/error messages as a dependable indicator of MetaDefender Core process crashes.
- **Do** implement **OS-level process/service monitoring** and forward **OS crash/service events** (Windows Event Log, journald/rsyslog) to your SIEM for alerting and correlation.
