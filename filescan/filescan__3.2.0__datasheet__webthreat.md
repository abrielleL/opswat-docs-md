<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/webthreat -->

# Web Threat Analyzer Overview

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Aether on-premise / standalone integrates with the following Web threat models

## [Introduction](/docs/filescan/3.2.0/datasheet/webthreat#introduction)

The Web Threat Analyser Model enhances security by analyzing a site’s structure, behavior, and content to label pages as malicious, based on sandbox verdicts. After gathering data, it makes predictions in milliseconds. It works in standalone environments but not in air-gapped systems.

## [Key Advantages Over Traditional Phishing Detection:](/docs/filescan/3.2.0/datasheet/webthreat#key-advantages-over-traditional-phishing-detection)

**More Accurate Detection**: Traditional phishing detection typically relies on URL reputation or known threat patterns, which can miss new or sophisticated attacks. This model checks multiple aspects of a site (structure, behavior, content), making it far more accurate at detecting threats.

**Real-Time Evaluation**: While traditional phishing detection often uses reputation data or blacklists, this model evaluates the site’s real-time behavior and content. This allows it to catch threats that don’t match known patterns or blacklisted URLs.

**Faster Predictions**: Predictions are made in milliseconds once the data is collected, ensuring quick threat identification compared to traditional methods, which can take longer due to live checks or scanning.

## [Operations](/docs/filescan/3.2.0/datasheet/webthreat#operations)

The model performs a comprehensive analysis on the collected data after sending a URL to the sandbox, including its structure, behavior, and content, to assess its safety, then generates a probability score indicating the likelihood of the URL being a web threat.

## [Report](/docs/filescan/3.2.0/datasheet/webthreat#report)

Web threat result will be displayed under URL details tab in the scan report. Key: **ML Web Threat Model**

## [Confidence mappings](/docs/filescan/3.2.0/datasheet/webthreat#confidence-mappings)

| Verdict | Description | Content model edges | Behavior model edges | Structure model edges |
| --- | --- | --- | --- | --- |
| Trusted | Content and structure appear normal, with no threat indicators. | 0.0 - 0.2 | 0.0 - 0.2 | 0.0 - 0.1 |
| No Threat Detected | Slight or minor deviations detected, but overall low risk. | 0.2 – 0.35 | 0.2 – 0.35 | 0.1 – 0.2 |
| Undetermined | Ambiguous or atypical features; unable to determine threat confidently. | 0.35 – 0.6 | 0.35 – 0.5 | 0.2 – 0.8 |
| Low Risk | Moderate to strong indicators suggesting potential phishing behavior. | 0.6 – 0.8 | 0.5 – 0.75 | 0.8 – 0.88 |
| High Risk | Strong resemblance to known phishing patterns. High probability of being harmful. | 0.8 – 0.9 | 0.75 – 0.9 | 0.88 – 0.95 |
| Confirmed Threat | Overwhelming match to malicious signatures. Immediate mitigation recommended. | 0.9 – 1.0 | 0.9 – 1.0 | 0.95 – 1.0 |

## [Available on the product](/docs/filescan/3.2.0/datasheet/webthreat#available-on-the-product)

## [Configuration](/docs/filescan/3.2.0/datasheet/webthreat#configuration)

Currently, it runs by default on every URL scan and triggers notifications to consumers if the likelihood prediction exceeds a threshold.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
