<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/scan-priorities -->

# Scan Priorities & Throughput Tuning

> **Info**
>
> Available in **MetaDefender Storage Security 3.6.0** and later.

This guide explains how MetaDefender Storage Security (MDSS) controls **how fast** your storages are scanned, and how you can tune that speed. It covers three settings:

- **Scan Priority** (Low / Medium / High)
- **Prefetch Count** (`RABBITMQ_DISCOVERY_PREFETCH_COUNT`, `RABBITMQ_SCANNING_PREFETCH_COUNT`, `RABBITMQ_REMEDIATIONS_PREFETCH_COUNT`)
- **Consumer Multiplier** (`RABBITMQ_CONSUMER_MULTIPLIER`)

No prior knowledge of the internals is required — everything is explained with a simple analogy and worked examples.

---

## How scanning works (in one minute)

When MDSS scans a storage, the work moves through an internal pipeline made up of three stages:

1. **Discovery** — MDSS walks through your storage and finds every file that needs to be scanned.
2. **Scanning** — each file found is then scanned for threats.
3. **Remediation** — when a file needs action (for example, a threat is found), MDSS applies the configured action to it, such as moving, deleting, or quarantining the file.

All three stages process files using parallel **workers**. The settings in this guide simply control **how many workers run** and **how much work each worker holds at a time**.

> **Info**
>
> Moving-team analogy — used throughout this guide. Think of scanning your files like a team clearing a pile of boxes:
>
> - Workers (Consumer Multiplier) = how many movers are working.
> - Prefetch Count = how many boxes each mover carries per trip.
> - Scan Priority = how many movers you put on a job.
>
> More movers, each carrying more per trip = the pile clears faster — as long as you have enough people (your server's CPU and memory) to keep up.

---

## 1. Scan Priority (Low / Medium / High)

Every scan you start is given a **priority**. The priority decides how much processing power that scan receives relative to other scans. Higher-priority scans are automatically assigned **more parallel workers**, so they finish faster.

| Priority | Relative processing power | Best for |
| ---- | ---- | ---- |
| **Low** *(default)* | Baseline | Routine, scheduled, or background scans where finishing time isn't critical |
| **Medium** | 3× the workers of Low | Standard on-demand scans a user is actively waiting on |
| **High** | 6× the workers of Low | Urgent, time-sensitive scans that must complete as quickly as possible |

Key things to know:

- **Low is the default.** If you don't choose a priority, the scan runs as Low.
- **Priority is set per scan.** Two scans on the same storage can run at different priorities at the same time.
- **Higher priority does not pause lower-priority scans.** All priorities run in parallel — High simply gets many more workers, so it drains its queue much faster and effectively finishes ahead.

---

## 2. Prefetch Count

**What it is:** the number of files a **single worker** pulls and holds at one time before reporting them as done.

In the moving-team analogy, this is how many boxes each mover carries per trip. Carrying more per trip means fewer empty-handed walks back — the mover keeps working instead of waiting for the next box.

| Setting | Controls | Default | Maximum |
| ---- | ---- | ---- | ---- |
| `RABBITMQ_DISCOVERY_PREFETCH_COUNT` | Discovery stage (finding files) | 10 | 400 |
| `RABBITMQ_SCANNING_PREFETCH_COUNT` | Scanning stage (scanning files) | 10 | 400 |
| `RABBITMQ_REMEDIATIONS_PREFETCH_COUNT` | Remediation stage (acting on files) | 10 | 400 |

**Effect of the value:**

- **Too low (e.g. 1):** each worker finishes one file, then waits to be handed the next. Small idle gaps add up and reduce throughput.
- **Balanced (e.g. 10–50):** the worker always has the next files ready, so it never sits idle. Recommended for most deployments.
- **Too high (e.g. 400):** a single worker can hoard a large batch of files while other workers sit idle, and memory usage rises. Rarely beneficial.

> **Info**
>
> Example: `RABBITMQSCANNINGPREFETCH_COUNT=20` Each scanning worker keeps up to 20 files lined up. As soon as it finishes one, the next is already waiting — no time wasted asking for more work.

> **Info**
>
> Any value above the maximum (400) is automatically capped.

---

## 3. Consumer Multiplier

**What it is:** how many **workers** the service runs in parallel. This is how many movers you put to work at once.

| Setting | Default | Maximum |
| ---- | ---- | ---- |
| `RABBITMQ_CONSUMER_MULTIPLIER` | 1 | 10 |

**The important detail:** the multiplier is a **base number** that is automatically scaled up for higher priorities. You set one value, and MDSS applies it proportionally:

| Priority | Workers created |
| ---- | ---- |
| **Low** | multiplier × 1 |
| **Medium** | multiplier × 3 |
| **High** | multiplier × 6 |

> **Info**
>
> Example: `RABBITMQCONSUMERMULTIPLIER=2`
>
> - Low-priority scans → 2 workers
> - Medium-priority scans → 6 workers (2 × 3)
> - High-priority scans → 12 workers (2 × 6)

>

> **Info**
>
> This is exactly why High-priority scans are faster — they automatically receive 6× the workers of Low.

**When to increase it:** when scans are running slower than you'd like, files are clearly piling up, **and** your server still has spare CPU and memory. Each extra worker scans another file in parallel.

**When to leave it at the default (1):** most deployments. Raising it above 3–5 is rarely necessary and increases load on the system. Any value above the maximum (10) is automatically capped.

---

## 4. Putting it all together

The total number of files a stage can process **at once** is:

```plaintext
workers × prefetch count
```

Remember that the number of **workers** depends on both the multiplier *and* the priority (Low ×1, Medium ×3, High ×6).

### A step-by-step tuning walkthrough

The best way to understand these settings is to follow a real tuning session. Imagine a customer scanning a large file share. We start with the out-of-the-box defaults and adjust one thing at a time, checking the effect after each change.

#### Iteration 0 — Start with the defaults

```plaintext
RABBITMQ_CONSUMER_MULTIPLIER     = 1   (default)
RABBITMQ_SCANNING_PREFETCH_COUNT = 10  (default)
```

Files the Scanning stage can process at once, per priority:

| Priority | Workers (multiplier × tier) | Prefetch each | Files in progress at once |
| ---- | ---- | ---- | ---- |
| **Low** | 1 (1×1) | 10 | **10** |
| **Medium** | 3 (1×3) | 10 | **30** |
| **High** | 6 (1×6) | 10 | **60** |

> **Info**
>
> Observation: A High-priority scan completes reasonably fast, but a large Low-priority scan feels slow. Checking the server, CPU and memory still have plenty of headroom — so there's room to push harder.

#### Iteration 1 — Increase the prefetch count

Each worker is finishing its files and then waiting for the next batch. We give every worker a bigger armful by raising the prefetch count from 10 to 20:

```plaintext
RABBITMQ_CONSUMER_MULTIPLIER     = 1
RABBITMQ_SCANNING_PREFETCH_COUNT = 20   ← changed
```

| Priority | Workers | Prefetch each | Files in progress at once |
| ---- | ---- | ---- | ---- |
| **Low** | 1 | 20 | **20** *(was 10)* |
| **Medium** | 3 | 20 | **60** *(was 30)* |
| **High** | 6 | 20 | **120** *(was 60)* |

> **Info**
>
> Observation: Throughput roughly doubles and workers no longer sit idle between files. But the Low-priority scan still isn't keeping up with demand, and the CPU is still not fully used. The bottleneck now is the number of workers, not how much each one holds.

#### Iteration 2 — Increase the consumer multiplier

We add more workers by raising the multiplier from 1 to 2. This doubles the workers at **every** priority:

```plaintext
RABBITMQ_CONSUMER_MULTIPLIER     = 2    ← changed
RABBITMQ_SCANNING_PREFETCH_COUNT = 20
```

| Priority | Workers (multiplier × tier) | Prefetch each | Files in progress at once |
| ---- | ---- | ---- | ---- |
| **Low** | 2 (2×1) | 20 | **40** *(was 20)* |
| **Medium** | 6 (2×3) | 20 | **120** *(was 60)* |
| **High** | 12 (2×6) | 20 | **240** *(was 120)* |

> **Info**
>
> Observation: Scanning is now fast at every priority — a High scan can move up to 240 files through scanning at once, 6× a Low scan. The CPU is now well used but not maxed out, which is the healthy target.

#### Iteration 3 — Tune the other stages if needed

Scanning is no longer the bottleneck, but the customer notices that after scanning, **acting on flagged files (remediation) is lagging behind**. Each stage has its own prefetch count, so we raise the remediation stage too:

```plaintext
RABBITMQ_CONSUMER_MULTIPLIER          = 2
RABBITMQ_SCANNING_PREFETCH_COUNT      = 20
RABBITMQ_REMEDIATIONS_PREFETCH_COUNT  = 20   ← changed
RABBITMQ_DISCOVERY_PREFETCH_COUNT     = 20   ← optional, if finding files is also slow
```

> **Info**
>
> Observation: The whole pipeline — finding, scanning, and acting on files — now flows smoothly. Note that `RABBITMQCONSUMERMULTIPLIER` is a single setting that applies to all stages, while each stage has its own prefetch count, so you can fine-tune any stage independently.

#### When to stop

Keep increasing only while the queues are backing up **and** the server still has spare CPU and memory. The moment CPU approaches 80%, stop — adding more workers to a maxed-out server makes things slower, not faster. At that point the answer is more hardware, not bigger numbers.

---

## 5. Quick reference

| You want to… | Do this |
| ---- | ---- |
| Finish a specific scan faster | Start it as **High** priority (6× the workers) |
| Run a non-urgent background scan | Leave it as **Low** (the default) |
| Speed up scanning overall (CPU has headroom) | Increase `RABBITMQ_CONSUMER_MULTIPLIER` |
| Smooth out workers that idle between files | Increase the relevant `*_PREFETCH_COUNT` |
| Speed up the **finding** of files | Tune `RABBITMQ_DISCOVERY_PREFETCH_COUNT` |
| Speed up the **scanning** of files | Tune `RABBITMQ_SCANNING_PREFETCH_COUNT` |
| Speed up **acting on** flagged files | Tune `RABBITMQ_REMEDIATIONS_PREFETCH_COUNT` |

### Default and maximum values

| Setting | Default | Maximum |
| ---- | ---- | ---- |
| `RABBITMQ_DISCOVERY_PREFETCH_COUNT` | 10 | 400 |
| `RABBITMQ_SCANNING_PREFETCH_COUNT` | 10 | 400 |
| `RABBITMQ_REMEDIATIONS_PREFETCH_COUNT` | 10 | 400 |
| `RABBITMQ_CONSUMER_MULTIPLIER` | 1 | 10 |

### Important notes

- **These settings increase parallelism, not raw machine speed.** They help only when workers are waiting for work while your CPU and memory still have room to spare. On a server that is already at full CPU, raising these values will **not** help — add more resources instead.
- **Changing the environment variables requires a service restart** to take effect. Set them in the service's environment configuration (`.env` / `customer.env`).
- **Values above the maximum are automatically capped** to the limits shown above.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
