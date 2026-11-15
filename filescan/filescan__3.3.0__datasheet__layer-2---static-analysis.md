<!-- source: https://www.opswat.com/docs/filescan/3.3.0/datasheet/layer-2---static-analysis -->

# Layer 2 - Static Analysis

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/filescan/3.3.0/datasheet/layer-2---static-analysis#overview)

Predictive Alin AI is OPSWAT’s proprietary malware detection engine for pre-execution file analysis. It runs in parallel with the Metascan multiscanning package to help identify malicious files before detonation or endpoint execution.

At a glance

- Best for: high-volume enterprise file flows
- Implemented: before execution (static analysis)
- Helps with: unseen, low-prevalence, and structurally modified malware
Why it matters

**Predictive Alin AI** helps close the gap between malware emergence and signature availability by making a prediction before execution.

## [What it’s designed for](/docs/filescan/3.3.0/datasheet/layer-2---static-analysis#what-its-designed-for)

Predictive Alin AI is built for high-volume enterprise environments and focuses on threats that are often underrepresented in signature-first models, including:

- Previously unseen variants
- Low-prevalence malware
- Structurally modified or obfuscated samples

## [Primary use cases](/docs/filescan/3.3.0/datasheet/layer-2---static-analysis#primary-use-cases)

Organizations typically use Predictive Alin AI to strengthen pre-execution controls in workflows that process large volumes of inbound and outbound files, for example, to:

- Reduce exposure to emerging malware variants
- Increase consistency of **allow / block / quarantine** policy enforcement
- Maintain detection performance at operational scale

## [How it works (high level)](/docs/filescan/3.3.0/datasheet/layer-2---static-analysis#how-it-works-high-level)

Predictive Alin AI evaluates intrinsic file characteristics using machine learning models, rather than relying exclusively on signature or hash matches. This improves detection coverage for patterns that may not yet be represented in traditional signature catalogs.

The analysis is **static and pre-execution**, which supports high-throughput environments where detonation is not always operationally practical.

## [Supported scope](/docs/filescan/3.3.0/datasheet/layer-2---static-analysis#supported-scope)

- Platforms: Windows, Linux
- File types: PE, ELF, MACHO, PDF

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
