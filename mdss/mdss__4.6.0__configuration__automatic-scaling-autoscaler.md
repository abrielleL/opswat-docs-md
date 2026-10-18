<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/automatic-scaling-autoscaler -->

# Automatic Scaling (Autoscaler)

MetaDefender Storage Security (MDSS) continuously monitors its own workload and automatically adjusts how much data it processes at once, so scans keep moving during busy periods and resources are freed up when activity is low. This happens on its own, with no manual setup.

This page explains what automatic scaling does, the optional setting you can tune, what you can see on the built-in **System** dashboard, the recommendations it may show you, and how to turn it off if you need to.

## Overview

The amount of work flowing through MDSS rises and falls throughout the day as files are discovered, scanned, and remediated. Automatic scaling (the "autoscaler") keeps performance steady across those changes.

Its goal is to process your files as fast as possible while keeping the system stable, by using the resources available to it as fully and efficiently as it can. Instead of running at a fixed pace, MDSS watches how busy the system is and adjusts how much work it processes in parallel. When there is work to do and capacity to spare, it raises throughput to get the most out of your hardware. When a resource approaches its limit, it settles at the highest rate that resource can sustain. When the backlog is cleared, it releases the resources it no longer needs.

Automatic scaling makes the resources you already have work as efficiently as possible. It does not add or remove servers on its own. When it detects that more capacity is needed, it tells you what to add through on-screen recommendations.

Automatic scaling is enabled by default and works out of the box. No setup is required.

## How it works

Automatic scaling checks the system every few seconds and adjusts how much work MDSS takes on, so the available resources are used as fully as they can be without putting the system at risk.

MDSS pays attention to indicators such as:

- how busy the processors (CPU) and memory are,
- how large the backlog of waiting work is,
- how quickly scans are being completed,
- the health and responsiveness of connected MetaDefender Core scan instances, and
- available disk space.

Based on these, its behavior is deliberately smooth and cautious:

- **It raises throughput** when there is a backlog and spare capacity, using more of the available resources to clear work faster.
- **It settles at a sustainable level** when a resource comes under sustained pressure, running it at the highest rate it can sustain instead of overcommitting it and risking instability.
- **It throttles to protect the system** when a resource reaches a critical limit. This can happen when CPU or memory runs out of headroom, when the output pipeline cannot drain as fast as new work arrives, or when a connected MetaDefender Core scan instance is overloaded (its scan queue is nearly full) or is returning scan errors. In these situations MDSS reduces how much it takes on so that processing stays reliable and errors are avoided, then ramps back up once the pressure clears. An instance that only turns requests away because it is busy makes MDSS ease back gradually rather than throttle.
- **It rests when idle**, returning to a light baseline once the backlog is cleared so resources are free for other work.

### Built-in safety guardrails

Separately from performance tuning, MDSS includes a safety guardrail that protects your data and the system. If free disk space becomes critically low, MDSS automatically **pauses** processing so the system does not run out of room, and **resumes** automatically once space is recovered. When this happens, it shows a message explaining what to do.

---

## Desired load for MetaDefender Core instances

Every MetaDefender Core scan instance has a queue with a maximum size. **Desired load** is the share of that queue MDSS aims to keep filled on that instance.

You do not need to set it. Automatic scaling works without it and the default suits most deployments. It exists so that a deployment whose MetaDefender Core instances differ in size can give each one an appropriate amount of work, instead of applying a single value everywhere.

### Where to find it

Go to **Settings > Scan Pools**, open a pool that holds MetaDefender Core instances, then add or edit an instance. The field is **Desired load (%)**. The current value also appears in the **Desired load (%)** column of the pool's instance list.

It appears for MetaDefender Core instances only. MetaDefender Cloud and MetaDefender Core Cluster instances do not expose a queue maximum to aim at, so the setting does not apply to them.

![](https://uploads.developerhub.io/prod/k8zL/id9ah2v964t38vemv53ewln3qiz7q9gylofejz5nnz9ex2d9qkakqbyyykc5jqxb.png)

### Accepted values

The value must be between **20 and 80**. The default is **40**, the value MDSS is tested against. The higher you set it, the more files MDSS sends to that instance at the same time.

MDSS increases the rate at which it sends files only while each instance's queue is below its desired load by more than a small margin, 10 percentage points by default. The minimum of 20 keeps an idle instance outside that margin, so it never stops MDSS from ramping up. The maximum of 80 leaves room below 95% of the queue, the point at which MDSS treats the instance as critically loaded, so MDSS can ease off gradually instead of braking sharply.

A change takes effect within seconds, with no restart.

### Choosing a value

Leave it at 40 unless you have a reason to change it.

Raise it when the instance has capacity to spare. Above 60 the product shows a caution: "At this level MDSS sends many files to MetaDefender Core at once. An undersized Core can saturate and scan times may grow."

![](https://uploads.developerhub.io/prod/k8zL/wa74j51v4eyzjteoqlrilqrzdl1l35dn4btba40xcaw36c29sp28i3q527j8bg2i.png)

Lower it when the instance is struggling. MDSS uses the desired load to decide when to stop sending more, so a lower value makes it stop increasing sooner. If MDSS decides the desired load is too high for that instance, it says so on the **System** dashboard and recommends returning it to 40; see [Recommendations you may see](#recommendations-you-may-see).

![](https://uploads.developerhub.io/prod/k8zL/0nmvew7bbb3l3cfsfuwwximxx0eijgp0o4msxldcdq4c978j7qwlcd7goquukr0u.png)

## The System dashboard

MDSS includes a **System** dashboard that shows, in real time, what automatic scaling is doing and why. It refreshes automatically every few seconds. The dashboard is for monitoring only; the system tunes itself, so there is nothing to configure here.

The dashboard appears as a **System** tab alongside the main **Dashboard** view, for users with the Administrator or SSO Administrator role.

![](https://uploads.developerhub.io/prod/k8zL/g9jbddb3scenyv8xtg9tkrq2rd9e8424566hufvbuev7wesyuss9svqjvmczpv2f.png)

### Autoscaling insight

The top card summarizes, in a single sentence, what MDSS is doing right now. Examples include *"I'm scaling up to keep scanning moving while you review this,"* and *"I'm continuously verifying your deployment."* When there is something to address, it explains the cause in plain language and marks how urgent it is **(Action required**, **Recommended**, or **Worth reviewing**). When everything is healthy, it confirms that no action is needed.

![](https://uploads.developerhub.io/prod/k8zL/lhe1phhhehprbpr74bxenpwaqsea92uu58xlhqep405987cuv2xd5cz8d9iw5jrx.png)

### Live status

A strip of key figures gives a quick summary: how many scans are in progress, the current status (such as **Scaling up** or **Idle**), what is currently limiting performance (if anything), and how many files are being processed per minute. A **History** button opens a timeline of recent activity.

![](https://uploads.developerhub.io/prod/k8zL/k2ihuslpkip5srt8sp1lpkx9v2b781waler2ep0b68pkkyelnjl2gap5dnt5gagb.png)

### Autoscaling activity

A running timeline of notable events, such as speeding up, slowing down, or pausing. Each event is described in plain language, for example *"MDSS increased scanning throughput to keep up with incoming files."*

> ![](https://uploads.developerhub.io/prod/k8zL/8jryxhjjzs35hrze1a18qtsg9ijxiqcptl0imixediktvu0r203k3i2hye12k6al.png)

### Resource utilization

Cards show current usage of CPU, memory, disk, database, and cache, each with a healthy, warning, or critical indicator.

> ![](https://uploads.developerhub.io/prod/k8zL/5atzyzlffs5v2qxjw2j1ddvwjdevcpgjjq18p9igeztthf0l1tyyjo4e9hcdqhr6.png)

### Throughput & queue pressure

Shows how much work is waiting at each stage and lets you switch between two live charts: **Throughput** (files processed per minute over time) and **Queue pressure** (backlog size over time). This makes it easy to see whether MDSS is keeping up with incoming work.

> ![](https://uploads.developerhub.io/prod/k8zL/inzlmhwdoqd418q6ufv1dflzbwsh13okfzabe2e4j3s98dpzinqokobg491zklub.png)

### Service health

Shows the health of each MDSS service, with a summary of how many are healthy, each service's current processing rate, and a short explanation of any bottleneck.

> ![](https://uploads.developerhub.io/prod/k8zL/qon6k6npm1sml8989eupi771n46vw2mk9gt8af8xqk2j51kcniafgpcgom1154wn.png)

### MetaDefender Core instances

A table of the MetaDefender Core scan instances currently used by the active jobs, showing each instance's address, health status, and current processing rate. An instance that is holding back overall performance is flagged as a bottleneck.

A **Reason** column explains why: the instance is overloaded, is returning scan errors, or is rate-limited. When the reason is scan errors or rate limiting and the instance's desired load is above the default of 40, the **Autoscaling insight** card at the top of the dashboard also names the instance and its desired load.

> ![](https://uploads.developerhub.io/prod/k8zL/ec69w8h72hzpvr5cmgrvgz7q71mk5cmm96fwuzw58dn4iggrbg29vl9psz2ab7q9.png)

### Processing status

When the safety guardrail is active, a card shows whether processing is **Normal** or **Paused**, along with the reason and the current disk space status. If processing is paused, MDSS also shows a banner and a recommended action to resolve it.

> ![](https://uploads.developerhub.io/prod/k8zL/p1ebomkra59bj8xh2u21125jhzooxw9cw1zg9hoomcmuoj83evp5nwby4hmh2qyk.png)

### Status indicators elsewhere

Beyond the System dashboard, a compact status card appears in the sidebar. If performance becomes degraded, a banner appears across the application with a link to the recommended actions, so you are kept informed even when you are not viewing the dashboard.

![](https://uploads.developerhub.io/prod/k8zL/07t3sj3k6ej3pjle04ll1u4ig1a49gigpir1gh8upd4uif592yej4e2mtl97oqii.png)

---

## Autoscaling states

The **Status** on the dashboard reflects what automatic scaling is doing at that moment:

| State | Meaning |
| ---- | ---- |
| **Idle** | Little or no work to do. MDSS is running at a light baseline to conserve resources. |
| **Scaling up** | Demand is high and resources are available, so MDSS is increasing how much it processes at once. |
| **Holding** | Conditions are near a limit, so MDSS is holding steady rather than changing course. |
| **Scaling down** | A resource is under sustained pressure, so MDSS is easing back to relieve it. |
| **Throttling** | A resource has reached a critical limit, so MDSS is temporarily processing less at once to keep things reliable and avoid errors. It ramps back up automatically once the pressure clears. See the **How it works** section for the situations that trigger this. |
| **Paused** | The safety guardrail has paused processing to avoid running out of disk space. Processing resumes automatically once space is recovered. |

---

## Recommendations you may see

When MDSS determines that your hardware or a supporting component has become the limiting factor, it shows a single, prioritized recommendation. Recommendations are advisory. MDSS keeps running as efficiently as it can, and acting on a recommendation should improve performance or resolve a constraint.

| Recommendation | Why you are seeing it | What to do |
| ---- | ---- | ---- |
| **Increase specs** | The MDSS host is below the minimum recommended hardware. | Bring the host up to the [minimum recommended CPU and memory](https://www.opswat.com/docs/mdss/getting-started/general-system-requirements). |
| **Increase CPU** | Performance is being held back by available CPU. | Add CPU to the host, or add an additional MDSS instance to share the load. |
| **Increase memory** | Performance is being held back by available memory. | Add memory to the host, or add an additional MDSS instance. |
| **Use an external database** | The database is limiting throughput or growing large on the local host. | Move the database to a [dedicated external host](https://www.opswat.com/docs/mdss/installation/external-services-configuration#postgresql-configuration). |
| **Use an external cache** | The local cache is limiting throughput. | Move the cache to a [dedicated external host](https://www.opswat.com/docs/mdss/installation/external-services-configuration#redis-configuration). |
| **Use an external MetaDefender Core** | The local MetaDefender Core is limiting scan throughput. | Switch to an external MetaDefender Core so scanning can scale independently. |
| **Increase MetaDefender Core performance** | Your external MetaDefender Core is at capacity. | Increase its resources or add more Core nodes. |
| **Lower the target load on this MetaDefender Core instance** | A MetaDefender Core instance is returning scan errors or turning requests away, and its desired load is set above the default. | Set that instance's desired load back to 40. |
| **Increase storage** | Processing was paused because disk space or database capacity is critically low and the database runs on an external host. With a local database, MDSS shows **Use an external database** instead. | Free up or add disk space to resume processing. |

> MDSS shows the single most important recommendation at any time rather than a long list, so you can focus on the change that will have the greatest impact.

## Turning automatic scaling off

Automatic scaling is enabled by default, and we recommend leaving it on. If you need to turn it off, you can do so with an environment variable:

```plaintext
SCANNING_AUTOSCALER_ENABLED=false
```

With this set, MDSS stops adjusting how much it processes and runs at a steady baseline instead. It continues to monitor performance and show the dashboard. Restart MDSS for the change to take effect.

> **Note:** The safety guardrail that pauses processing when disk space is critically low stays active regardless of this setting, so the system stays protected even when automatic scaling is turned off.

## Frequently asked questions

**Does automatic scaling add or remove servers?** No. It makes your existing deployment work as efficiently as possible. When more capacity is needed, it recommends what to add rather than provisioning it for you.

**Does automatic scaling slow down my scans?** No. It works to complete your scans as fast as possible by using the available system resources as fully and efficiently as it safely can. If a resource reaches a critical limit, MDSS temporarily processes less at once (throttling). This keeps scanning reliable and prevents the system from being overloaded, which would otherwise cause errors or instability. Once the pressure clears, MDSS ramps back up.

**Do I need to configure anything to use it?** No. It is enabled by default and self-tuning. There is one optional value, the desired load for each MetaDefender Core scan instance, which has a working default. See [Desired load for MetaDefender Core instances](#desired-load-for-metadefender-core-instances).

**Why does processing sometimes pause?** The safety guardrail pauses processing when disk space becomes critically low, and resumes automatically once space is recovered. Follow the on-screen **Increase storage** recommendation to resolve it.

**Why am I seeing a recommendation to add hardware or move a component externally?** Because MDSS has determined that resource is currently limiting performance.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
