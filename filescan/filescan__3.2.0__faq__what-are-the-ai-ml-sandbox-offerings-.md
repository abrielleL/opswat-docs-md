<!-- source: https://www.opswat.com/docs/filescan/3.2.0/faq/what-are-the-ai-ml-sandbox-offerings- -->

# What are the AI/ML Aether offerings?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Introduction](/docs/filescan/3.2.0/faq/what-are-the-ai-ml-sandbox-offerings-#introduction)

The AI/ML Aether offerings enhance threat detection and analysis through a suite of advanced machine learning technologies integrated into the sandbox environment. These solutions are designed to uncover sophisticated threats, including zero-day malware, phishing sites, and malicious URLs, which often evade traditional defenses.

## [AI/ML features:](/docs/filescan/3.2.0/faq/what-are-the-ai-ml-sandbox-offerings-#aiml-features)

**Threat Pattern Correlator**: Similarity Search leverages advanced feature extraction techniques to identify and correlate unknown threats with known malware families. By analyzing behavioral patterns, code structures, and static attributes, our machine learning models detect even evasive or zero-day threats that traditional signature-based methods may miss.

More Info: [Threat Pattern Correlator - Introduction](/docs/filescan/3.2.0/datasheet/threat-pattern-correlator)

**URL Reputation Predictor:** The offline URL detection ML model enhances security by effectively identifying suspicious URLs

More Info: [URL Reputation Predictor Overview](/docs/filescan/3.2.0/datasheet/offline-url-reputation)

**Brand Spoofing Detector**: Utilizing full Chrome-based webpage rendering combined with machine learning-driven image analysis, the platform detects phishing attempts by scrutinizing visuals for impersonations of over 338 major brands.

More Info: [ML Brand Detection](/docs/filescan/3.2.0/datasheet/url-capabilities)

**Web Threat Analyzer**: Web Threat Detection Model enhances security by analyzing a website’s structure, behavior, and content to label pages as malicious, based on sandbox verdicts. After gathering data, it makes predictions in milliseconds. It works in standalone environments, but not in air-gapped systems.

More Info: [Web Threat Analyzer Overview](/docs/filescan/3.2.0/datasheet/webthreat)

**ChatGPT Integration**: The primary aim of this executive summary is to make threat analysis easier to understand by highlighting the most significant aspects of the malware report.

More Info: [Chat GPT](/docs/filescan/3.2.0/configuration/chat-gpt)

## [Sandbox offerings](/docs/filescan/3.2.0/faq/what-are-the-ai-ml-sandbox-offerings-#sandbox-offerings)

| AI/ML services | MetaDefender Sandbox (Online) / Adaptive Sandbox for MD Cloud | MetaDefender Sandbox (Offline) | Adaptive Sandbox for MD Core (Embedded) | Enabled by default |
| --- | --- | --- | --- | --- |
| **Threat Pattern Correlator** | Yes | No | No | No |
| **URL Reputation Predictor** | Yes | Yes | Yes | No |
| **Brand Spoofing Detector** | Yes | No | No | Yes |
| **Web Threat Analyzer** | Yes | No | No | Yes |
| **ChatGPT Integration** | Yes | No | Yes | No |

## [Aether offerings](/docs/filescan/3.2.0/faq/what-are-the-ai-ml-sandbox-offerings-#aether-offerings)

| AI/ML services | MetaDefender Aether (Online) / Adaptive Sandbox for MD Cloud | MetaDefender Aether (Offline) | MetaDefender Aether for Core (Embedded) | Enabled by default |
| --- | --- | --- | --- | --- |
| **Threat Pattern Correlator** | Yes | No | No | No |
| **URL Reputation Predictor** | Yes | Yes | Yes | No |
| **Brand Spoofing Detector** | Yes | No | No | Yes |
| **Web Threat Analyzer** | Yes | No | No | Yes |
| **ChatGPT Integration** | Yes | No | Yes | No |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
