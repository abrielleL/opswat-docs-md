<!-- source: https://www.opswat.com/docs/mdinsights/feeds/metadefender-insights-osint -->

# MetaDefender InSights OSINT

## [About MetaDefender InSights OSINT feeds](/docs/mdinsights/feeds/metadefender-insights-osint#about-metadefender-insights-osint-feeds)

InSights OSINT is a threat indicator feed composed of indicators relating to adversary infrastructure used for a variety of abuse including phishing, malware staging, and attack origination including mail delivery. This feed includes data extracted from OPSWAT's proprietary processing and analysis of initial access payloads combined with our broad collection of open source intelligence (OSINT) sources.

### [Indicator types](/docs/mdinsights/feeds/metadefender-insights-osint#indicator-types)

InSights OSINT comprises the following types of threat indicators:

- Domain names

Indicator types

Upcoming InSights OSINT feeds will encompass additional indicator types such as URLs.

Target use case

This feed is well suited for broad-based threat intelligence workflows and threat detection programs. Thanks to extraction of indicators from our corpus of malicious initial access file payloads, network defense teams may find it useful as an early warning IOC feed useful to identify and quickly respond to attacker attempts to gain a foothold on end user devices.

### [Methodology](/docs/mdinsights/feeds/metadefender-insights-osint#methodology)

InSights OSINT comprises data collected from OPSWAT's backend file processing systems, including samples collected from [InQuest Labs](https://labs.inquest.net/). As we collect and process malicious files, we perform [Deep File Inspection](https://inquest.net/blog/an-introduction-to-deep-file-inspection/) (DFI) on files and extract network indicators from processed files. We additionally aggregate indicators collected from open source intelligence (OSINT) sources. These data sources are then analyzed and correlated, producing a dataset that captures the intersection of these indicators. The most highly ranked overlaps between files and OSINT indicators, and OSINT indicators sharing the most common sources, are assembled. After collecting and normalizing the data, our quality processing systems perform filtering and expiration of aged indicators, helping keep the resulting technical indicator feeds relevant and actionable for a broad range of uses.

### [Target systems](/docs/mdinsights/feeds/metadefender-insights-osint#target-systems)

Our InSights OSINT feed is suited for usage in SIEM platforms, XDR solutions, EDR and NDR deployments and email security platforms. Collecting the data in threat intelligence platforms (TIPs) can help ensure a comprehensive collection of early warning indicators appearing in OSINT data sources, but with a much tighter quality level than unfiltered collections alone.
