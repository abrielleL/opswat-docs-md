<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/autoscaler-environment-variables -->

# Automatic scaling settings

MetaDefender Storage Security (MDSS) adjusts how much it processes automatically, based on how busy the system is. This page lists the settings that control that behavior, with their default values and a short explanation of each one. For an overview of how automatic scaling works, see the [Automatic Scaling page](https://www.opswat.com/docs/mdss/configuration/automatic-scaling--autoscaler-).

Altering these settings is optional. They are provided for cases where you want to adapt the behavior to a specific environment. Each setting is applied as an environment variable. MDSS reads them when the service starts, so restart MDSS after making a change. The settings that control scaling apply to the scanning part of MDSS, which is why their names begin with `SCANNING_AUTOSCALER_`.

---

## 1. General behavior

| Setting | Default | Unit | What it does |
| ---- | ---- | ---- | ---- |
| `SCANNING_AUTOSCALER_ENABLED` | `true` | on/off | Turns automatic scaling on or off. When off, MDSS still monitors performance and shows the dashboard, but it no longer adjusts how much it processes by itself. |
| `SCANNING_AUTOSCALER_PROBE_INTERVAL` | `10` | seconds | How often MDSS checks the system and decides whether to adjust. |
| `SCANNING_AUTOSCALER_INITIAL_PREFETCH` | `20` | items | How many items each scanning worker starts with, and the level it returns to when there is no work. |
| `SCANNING_AUTOSCALER_MIN_PREFETCH` | `5` | items | The fewest items a worker will handle at once when scaling down. |
| `SCANNING_AUTOSCALER_MAX_PREFETCH` | `200` | items | The most items a worker will handle at once when scaling up. MDSS will not go above 200 by default, and never above an internal maximum of 400 even if you set a higher number. |
| `SCANNING_AUTOSCALER_IDLE_RESET_TICKS` | `30` | checks | How many quiet checks in a row before MDSS returns to its starting level. At the default check interval this is about five minutes. |
| `SCANNING_AUTOSCALER_THROTTLE_DURATION` | `30` | seconds | After MDSS reaches a critical limit and pulls back, how long it waits before testing whether it can speed up again. |
| `SCANNING_AUTOSCALER_PROBES_COUNT_SCALEUP` | `5` | checks | How many healthy checks in a row are needed before MDSS speeds up. A higher number makes it ramp up more cautiously. |
| `SCANNING_AUTOSCALER_PROBES_COUNT_SCALEDOWN` | `2` | checks | How many warning checks in a row before MDSS eases back. A lower number makes it back off sooner. |
| `SCANNING_AUTOSCALER_LOCAL_HARDWARE_HYSTERESIS` | `5.0` | percentage points | A small buffer around the CPU and memory limits that keeps MDSS from switching back and forth when usage sits right at a limit. |
| `SCANNING_AUTOSCALER_OUTBOUND_HYSTERESIS` | `5.0` | percentage points | The same kind of buffer for the queue of scanned results waiting for the next step. |
| `SCANNING_AUTOSCALER_DOWNSTREAM_HYSTERESIS` | `10.0` | percentage points | The same kind of buffer for how loaded the scan instances are. |

---

## 2. Resource limits

These set the points at which a resource is considered under pressure. When a resource passes its warning level, MDSS starts to ease back gradually. When it passes its critical level, MDSS reduces its load right away.

| Setting | Default | Unit | What it does |
| ---- | ---- | ---- | ---- |
| `SCANNING_AUTOSCALER_CPU_WARNING_THRESHOLD` | `90` | percent | CPU usage that MDSS treats as a warning. |
| `SCANNING_AUTOSCALER_CPU_CRITICAL_THRESHOLD` | `95` | percent | CPU usage that makes MDSS reduce its load immediately. |
| `SCANNING_AUTOSCALER_MEMORY_WARNING_THRESHOLD` | `80` | percent | Memory usage that MDSS treats as a warning. |
| `SCANNING_AUTOSCALER_MEMORY_CRITICAL_THRESHOLD` | `90` | percent | Memory usage that makes MDSS reduce its load immediately. |
| `SCANNING_AUTOSCALER_OUTBOUND_WARNING_THRESHOLD` | `70` | percent of the limit below | How full the results queue can get, as a percentage of the limit below, before MDSS treats it as a warning. |
| `SCANNING_AUTOSCALER_OUTBOUND_CRITICAL_THRESHOLD` | `9000` | items waiting | The number of scanned results waiting in the queue that makes MDSS reduce its load immediately. This is also the maximum size of that queue. |

The queue of incoming work has no limit to set. Any waiting work simply tells MDSS there is something to process.

---

## 3. Scan instance settings

These control how MDSS reads the load and health of the connected MetaDefender Core scan instances and how much work it sends to each one.

| Setting | Default | Unit | What it does |
| ---- | ---- | ---- | ---- |
| `SCANNING_AUTOSCALER_DOWNSTREAM_DESIRED_LOAD` | `40` | percent | The load MDSS aims to keep each scan instance at, as a percentage of what that instance can hold. |
| `SCANNING_AUTOSCALER_DOWNSTREAM_WINDOW_SIZE` | `100` | recent results | How many recent results MDSS looks at when judging how loaded a scan instance is. |
| `SCANNING_AUTOSCALER_DOWNSTREAM_CRITICAL_ERROR_RATE_THRESHOLD` | `0.10` | share (0 to 1) | The share of recent requests that fail before MDSS treats a scan insatnce as unhealthy and pulls work away from it. The default of `0.10` means 10 percent. |
| `SCANNING_AUTOSCALER_DOWNSTREAM_CRITICAL_ERROR_RATE_WINDOW_SIZE` | `100` | recent results | How many recent results are used for the failure-rate check above. |
| `SCANNING_AUTOSCALER_DOWNSTREAM_WARNING_429_RATE_THRESHOLD` | `0.10` | share (0 to 1) | The share of recent requests a scan instance turns away for being too busy before MDSS treats it as a warning. The default of `0.10` means 10 percent. |
| `SCANNING_AUTOSCALER_DOWNSTREAM_WARNING_429_RATE_WINDOW_SIZE` | `100` | recent results | How many recent results are used for the too-busy check above. |

---

## 4. Disk space protection

MDSS includes a safety guardrail that pauses processing when disk space runs low and resumes it once space is recovered. This protects your data and keeps working even when automatic scaling is turned off.

| Setting | Default | Unit | What it does |
| ---- | ---- | ---- | ---- |
| `GUARDRAILS_CHECK_INTERVAL_SECONDS` | `30` | seconds | How often MDSS checks available disk space. The lowest allowed value is 10. |
| `GUARDRAILS_USED_CRITICAL_PERCENT` | `90` | percent | How full the disk can get before MDSS pauses processing to avoid running out of space. |
| `GUARDRAILS_USED_RESUME_PERCENT` | `80` | percent | How far disk usage must drop before MDSS resumes processing. The gap below the pause level prevents rapid pausing and resuming. |
| `GUARDRAILS_DISK_MONITOR_PATH` | `/var/log/mdss` (Linux), install drive (Windows) | path | The disk location MDSS watches for free space. |
| `SCAN_INSTANCE_DISK_CRITICAL_THRESHOLD_PERCENT` | `5` | percent free | How little free disk space a scan instance can have before MDSS stops sending it work. |
| `SCAN_INSTANCE_HEALTH_JOB_INTERVAL_SECONDS` | `30` | seconds | How often MDSS checks the health of each scan instance. |
| `PERFORMANCE_MODE` | `false` | on/off | When set to `true`, turns off the disk space protection described here. Leave it off in normal use. |

---

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
