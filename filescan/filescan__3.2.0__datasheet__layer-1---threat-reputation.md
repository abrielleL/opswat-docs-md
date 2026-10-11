<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation -->

# Layer 1 - Threat Reputation

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Expose Known Threats Fast](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#expose-known-threats-fast)

**Threat Reputation is the first decision layer in MetaDefender Aether’s five-layer zero-day detection pipeline.**

Before Aether applies AI-powered prediction or dynamic analysis, Layer 1 determines whether a file or its associated infrastructure is already known.

Files and hashes, URLs, IP addresses, and domains are checked against continuously updated threat intelligence, online or offline. Known malicious indicators can be identified immediately, while unresolved files continue to deeper Aether analysis.

This gives Aether a fast first decision point that helps maintain file velocity while reserving more advanced analysis for threats that are genuinely unknown.

## [At a Glance](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#at-a-glance)

- **Purpose:** Identify known threats before deeper analysis
- **Checks:** File hashes, IP addresses, URLs, and domains
- **Threat intelligence:** 50+ billion indicators
- **Sources:** Up to 30 providers for IP, URL, and domain reputation
- **Operation:** Online or offline
- **Best for:** High-volume file flows, perimeter inspection, and restricted environments
- **Pipeline role:** Filter known threats before Predictive Alin AI and Adaptive Sandbox analysis

## [Why Layer 1 Matters](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#why-layer-1-matters)

Not every file needs AI analysis or sandbox execution.

A large part of effective zero-day detection is knowing when **not** to spend additional time and resources on a file.

Layer 1 performs the fastest check in the Aether pipeline by comparing indicators against known threat intelligence. When malicious infrastructure or a previously identified threat is recognized, Aether can make an earlier decision without immediately escalating the file to more resource-intensive analysis.

When reputation is unknown or inconclusive, the file continues to Layer 2 for Pre-Execution analysis.

The result is a more efficient pipeline that applies deeper analysis only when the available intelligence requires it.

## [Global Threat Intelligence at the Front of the Pipeline](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#global-threat-intelligence-at-the-front-of-the-pipeline)

Layer 1 is powered by MetaDefender Threat Intelligence, providing access to **50+ billion hashes, IP addresses, URLs, and domains**.

Threat Reputation can:

- Check IP addresses, URLs, and domains using up to 30 intelligence providers
- Correlate file hashes with millions of known applications and CVEs
- Identify known malicious infrastructure and previously observed threats
- Support individual or high-volume reputation lookups
- Continuously incorporate newly discovered IOCs and threat intelligence

This gives Aether immediate context about what the security community and OPSWAT intelligence already know before deeper analysis begins.

## [Online and Offline Threat Reputation](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#online-and-offline-threat-reputation)

Layer 1 is designed for both connected and restricted environments.

Online deployments can use continuously updated global intelligence for current reputation decisions.

Offline and air-gapped environments can maintain local reputation intelligence so sensitive files and indicators do not need to leave the protected environment for every security decision.

This makes Threat Reputation relevant across cloud, on-premises, regulated, and fully air-gapped Aether deployments.

## [How Layer 1 Fits Into the Aether Pipeline](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#how-layer-1-fits-into-the-aether-pipeline)

Aether progressively increases analysis depth as uncertainty increases.

**Layer 1: Threat Reputation**
Is this file or infrastructure already known?

**Layer 2: Static Analysis**
Does Predictive Alin AI identify malicious intent Pre-Execution?

**Layer 3: Dynamic Analysis**
What does the file actually do when Adaptive Sandbox analyzes its behavior?

**Layer 4: Threat Scoring**
How risky is the combined evidence?

**Layer 5: Threat Hunting**
What malware families, infrastructure, variants, or campaigns is the threat connected to?

Layer 1 removes known threats from the unknown-threat problem so the rest of the pipeline can focus its resources where they matter most.

## [Threat Intelligence That Gets Stronger](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#threat-intelligence-that-gets-stronger)

Threat Reputation is not a static list.

As later Aether layers uncover previously unknown malicious files, URLs, domains, IP addresses, and other Indicators of Compromise, those discoveries can strengthen Layer 1 reputation intelligence.

This creates an important feedback loop:

**Unknown Threat → Deeper Analysis → New IOC → Reputation Intelligence → Earlier Future Detection**

An indicator that required deeper investigation the first time it appeared can become a known threat signal the next time Aether encounters it.

Global Adaptive Sandbox telemetry also contributes newly discovered indicators to MetaDefender Threat Intelligence, helping enrich future lookups with additional context and threat correlations.

## [Disrupt Reusable Attack Infrastructure](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#disrupt-reusable-attack-infrastructure)

Layer 1 maps directly to the lower levels of the **Pyramid of Pain**, including hashes, IP addresses, and domains.

Threat Reputation helps disrupt attacks by:

- Identifying reused malware binaries through hash reputation
- Blocking known malicious URLs, IP addresses, and domains
- Identifying known phishing and malware delivery infrastructure
- Making previously discovered indicators less reusable
- Forcing attackers to rotate infrastructure and delivery paths
- Increasing the cost of maintaining commodity malware, phishing, and botnet operations

Attackers can change a hash or domain relatively easily, but every change costs time and infrastructure. Layer 1 makes that reuse increasingly ineffective.

## [The Role of Layer 1](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputation#the-role-of-layer-1)

Layer 1 answers the fastest question in the Aether pipeline:

**Do we already know this threat?**

If the answer is yes, Aether can act immediately.

If the answer is no, the file moves forward for Predictive Alin AI Pre-Execution analysis and, when needed, Adaptive Sandbox dynamic analysis.

**Layer 1 resolves what is known quickly, so the rest of Aether can focus on what is not.**

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
