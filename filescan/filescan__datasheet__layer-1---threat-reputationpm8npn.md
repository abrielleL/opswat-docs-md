<!-- source: https://www.opswat.com/docs/filescan/datasheet/layer-1---threat-reputationpm8npn -->

# Layer 5 - Threat Hunting

## Connect Threats to Campaigns

**Layer 5 turns an individual file detection into broader threat intelligence.**

Once Aether has identified and scored a suspicious file, Threat Hunting asks the next question:

**What else is this threat connected to?**

ML-powered similarity search and Threat Pattern Correlation compare the sample with known malware, behavioral patterns, infrastructure, and previously analyzed threats. This helps analysts identify related malware families, modified variants, shared attacker infrastructure, and campaign-level activity that may not be obvious from a single file alone.

Layer 5 moves Aether from **file verdict to attacker context**.

## At a Glance

- **Purpose:** Connect individual detections to related malware and campaigns
- **Core capabilities:** ML-powered similarity search and Threat Pattern Correlation
- **Correlates:** Code, behavior, infrastructure, IOCs, tactics, and related files
- **Helps identify:** Malware families, variants, clusters, and attacker campaigns
- **Best for:** Threat hunting, incident response, retroactive investigation, and campaign analysis
- **Pipeline role:** Add campaign-level context after Aether has detected and prioritized the threat

## Why Layer 5 Matters

Attackers rarely rely on a single file.

The same campaign may use multiple payloads, recompiled variants, different hashes, changing infrastructure, and slightly modified execution techniques.

Looking at each sample in isolation makes these changes effective. Layer 5 looks for the relationships that remain.

By correlating structural and behavioral similarities across samples, Aether can identify related threats even when attackers change obvious indicators such as hashes, filenames, or domains.

This helps analysts determine whether a new detection is:

- An isolated malicious file
- A modified version of known malware
- Part of an existing malware family
- Connected to shared attacker infrastructure
- One stage of a broader campaign

## ML-Powered Similarity Search

Similarity Search helps identify relationships between new and previously analyzed malware.

Instead of depending only on exact hashes or signatures, machine learning compares structural and behavioral characteristics to identify related samples.

This can reveal:

- Recompiled malware variants
- Polymorphic mutations
- Shared code sections
- Related payloads
- Similar behavioral patterns
- Previously unseen members of a known malware family

This is particularly useful when an attacker modifies a file enough to defeat hash-based detection but leaves core code or behavior intact.

## Threat Pattern Correlation

Threat Pattern Correlation goes beyond file similarity by connecting evidence across multiple analyses.

It can correlate:

- Malware families
- Behavioral IOCs
- Shared infrastructure
- URLs, domains, and IP addresses
- Loader and payload relationships
- Common tactics and techniques
- Infrastructure clusters
- Campaign-level activity

By bringing these relationships together, Layer 5 helps analysts see the broader attack pattern instead of manually pivoting across isolated reports and indicators.

## From Detection to Proactive Hunting

Layer 5 supports both **proactive and retroactive threat hunting**.

### Proactive Hunting

When Aether identifies a new malicious sample, analysts can use its code, behavior, IOCs, and infrastructure relationships to search for related activity elsewhere.

This helps answer questions such as:

- Have we seen a similar file before?
- Are other variants of this malware already present?
- Does this sample share infrastructure with known threats?
- Is this part of an active campaign?
- What other files should we investigate?

### Retroactive Analysis

New intelligence can also be applied to previously analyzed samples.

As new malware relationships and threat patterns become known, analysts can revisit historical data to identify older files that may be connected to the same campaign or malware family.

This allows new discoveries to improve understanding of past activity, not just future detections.

## How Layer 5 Fits Into the Aether Pipeline

Each Aether layer narrows uncertainty before Layer 5 expands the investigation outward.

**Layer 1: Threat Reputation**
Do we already know this threat?

**Layer 2: Static Analysis**
Does Predictive Alin AI identify malicious intent Pre-Execution?

**Layer 3: Dynamic Analysis**
What does the file actually do?

**Layer 4: Threat Scoring**
How risky is the combined evidence?

**Layer 5: Threat Hunting**
**What other malware, infrastructure, and campaigns is this threat connected to?**

Layer 5 takes everything learned in the earlier stages and uses it to uncover relationships beyond the individual sample.

## Intelligence That Goes Beyond Indicators

Threat hunting becomes more valuable when reputation data, behavioral evidence, and similarity signals are analyzed together.

Layer 5 can use:

- Sandbox-derived behavioral IOCs
- Runtime behaviors
- Threat scores
- Malware configuration data
- Structural similarity
- Code relationships
- Infrastructure indicators
- MITRE ATT&CK context
- Historical analysis results

This helps analysts move beyond simple IOC matching and investigate how threats are related by behavior and attacker tradecraft.

## Reduce Manual Investigation

Traditional threat hunting often requires analysts to move between sandbox reports, reputation services, SIEM searches, threat intelligence platforms, and external tools.

Aether brings similarity and pattern correlation into the same zero-day detection workflow.

This helps teams:

- Reduce manual pivoting between tools
- Find related malware faster
- Identify campaign relationships earlier
- Enrich SIEM and SOAR investigations
- Prioritize related samples for deeper investigation
- Turn individual detections into reusable threat intelligence

## How Layer 5 Raises the Cost for Attackers

Layer 5 targets the highest level of the **Pyramid of Pain: tactics, techniques, and procedures**.

Hashes, domains, and individual payloads are relatively easy for attackers to change. Their operating methods are much harder to replace.

By correlating malware families, shared behaviors, infrastructure, and repeated tradecraft, Layer 5:

- Detects relationships even when hashes and payloads change
- Exposes repeated attacker behavior across variants
- Connects isolated files to broader operations
- Makes minor payload modifications less effective
- Forces attackers to change tools, infrastructure, behaviors, and operating methods

At this level, evasion becomes much more expensive. Attackers can no longer rely on simply changing one indicator or recompiling one file.

## The Role of Layer 5

Layers 1 through 4 determine **what the file is and how much risk it presents**.

Layer 5 determines **what the threat is connected to**.

By combining ML-powered similarity search with Threat Pattern Correlation, Aether helps security teams move from isolated file detection to malware family identification, infrastructure correlation, and campaign-level threat intelligence.

**Layer 5 turns a single detection into a map of the broader attack.**

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
