<!-- source: https://www.opswat.com/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai- -->

# What is Predictive Alin AI?

## [Overview](/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai-#overview)

Predictive Alin AI is OPSWAT’s proprietary malware detection engine for pre-execution file analysis. It runs in parallel with the Metascan multiscanning package to help identify malicious files before detonation or endpoint execution.

At a glance

- Best for: high-volume enterprise file flows
- Implemented: before execution (static analysis)
- Helps with: unseen, low-prevalence, and structurally modified malware
Why it matters

**Predictive Alin AI** helps close the gap between malware emergence and signature availability by making a prediction before execution.

## [What it’s designed for](/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai-#what-its-designed-for)

Predictive Alin AI is built for high-volume enterprise environments and focuses on threats that are often underrepresented in signature-first models, including:

- Previously unseen variants
- Low-prevalence malware
- Structurally modified or obfuscated samples

## [Primary use cases](/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai-#primary-use-cases)

Organizations typically use Predictive Alin AI to strengthen pre-execution controls in workflows that process large volumes of inbound and outbound files, for example, to:

- Reduce exposure to emerging malware variants
- Increase consistency of **allow / block / quarantine** policy enforcement
- Maintain detection performance at operational scale

## [How it works (high level)](/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai-#how-it-works-high-level)

Predictive Alin AI evaluates intrinsic file characteristics using machine learning models, rather than relying exclusively on signature or hash matches. This improves detection coverage for patterns that may not yet be represented in traditional signature catalogs.

The analysis is **static and pre-execution**, which supports high-throughput environments where detonation is not always operationally practical.

## [Supported scope](/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai-#supported-scope)

- Platforms: Windows, Linux
- File types: PE, ELF, MACHO, PDF

## [Availability](/docs/mdcore/predictive-alin-ai/what-is-predictive-alin-ai-#availability)

Predictive Alin AI is available **only through MetaDefender products and solutions**.

Licensing

**Predictive Alin AI** requires separate licensing for **MetaDefender** to enable this module.
