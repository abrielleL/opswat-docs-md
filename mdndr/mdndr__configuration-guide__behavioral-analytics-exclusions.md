<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/behavioral-analytics-exclusions -->

# Behavioral analytics — exclusions

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → Behavioral analytics — exclusions

Exclude known-good hosts, ports, or domains from the behavioral detections. Use exclusions to reduce false positives.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Beaconing** | Exclusion lists for beaconing detection. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Data Exfiltration** | Exclusion lists for data-exfiltration detection. Source/destination IP prefixes and destination ports listed here are suppressed before exfiltration SQL evaluates upload ratios and byte thresholds. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Long Duration** | Exclusion lists for long-duration flow detection. Includes source/destination IP prefix exclusions and destination port suppressions. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Port Scan** | Exclusion lists for port-scan detection. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Connection Spray** | Exclusion lists for connection-spray detection. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Fast Flux** | Exclusion lists for fast-flux DNS detection. Domain suffixes listed here are suppressed before fast-flux SQL evaluates unique IP and TTL behavior. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Dga** | Exclusion lists for DGA detection. Source IP prefixes, domain suffixes, and TLDs listed here are suppressed before DGA SQL evaluates NXDOMAIN ratios and query volumes. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **DNS Tunneling** | Exclusion lists for DNS tunneling detection. Domain suffixes (a live LIKE ANY pattern filter) are suppressed before DNS tunneling SQL evaluates query length, subdomain count, and response size. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Suspicious Port** | Exclusion lists for suspicious-port (protocol/port-mismatch) detection. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |

#### [Behavioral analytics — exclusions: BeaconingExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-beaconingexclusions-sub-settings)

*Source/destination IP prefix and port exclusions for beaconing detection.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from beaconing detection. Use this for known benign internal agents, scanners, or telemetry sources that should not contribute to beaconing alerts. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ip Prefixes** | Destination IP address prefixes excluded from beaconing detection. Use this for known benign SaaS, update, or telemetry destinations. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ports** | Destination port numbers excluded from beaconing detection. | — | list of integer | — |

#### [Behavioral analytics — exclusions: DataExfiltrationExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-dataexfiltrationexclusions-sub-settings)

*Source/destination IP prefix and port exclusions for exfiltration.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from data-exfiltration detection. Use this for backup systems, data warehouses, or other known high-volume internal sources. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ip Prefixes** | Destination IP address prefixes excluded from data-exfiltration detection. Use this for approved backup, cloud storage, or replication destinations. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ports** | Destination port numbers excluded from data-exfiltration detection. Traffic to these ports is filtered before upload ratio and byte thresholds are evaluated. Each value must be a valid TCP/UDP port (1–65535). Default: empty (no exclusions). | — | list of integer | — |

#### [Behavioral analytics — exclusions: LongDurationExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-longdurationexclusions-sub-settings)

*IP prefix and port exclusions for long-duration flow detection. Long-lived flows to cloud infrastructure (e.g. AWS, GCP, Microsoft 365) reliably generate false positives.* ***IP prefix exclusions*** *suppress entire address spaces. Each prefix is rendered in SQL as dest_ip NOT LIKE '<prefix>%'. Use dotted IPv4 CIDR-boundary strings such as: - "34.64." — Google Cloud asia-east1 - "52.112." — Microsoft Teams* ***Port exclusions*** *suppress specific services regardless of destination IP.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Destination Ip Prefixes** | Destination IP address prefixes excluded from long-duration flow detection. Each entry is matched as a SQL LIKE prefix (e.g. '34.64.' matches any IP starting with '34.64.'). Do not include a trailing '%' — it is appended automatically. Use dotted IPv4 or IPv6 CIDR-boundary prefix strings. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from long-duration flow detection. Use this for known long-lived internal systems such as collectors, scanners, or replication sources. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ports** | Destination port numbers excluded from long-duration flow detection. | — | list of integer | — |

#### [Behavioral analytics — exclusions: PortScanExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-portscanexclusions-sub-settings)

*Source/destination IP prefix and port exclusions for port-scan detection.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from port-scan detection. Use this for approved scanners, monitoring systems, or management networks. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ip Prefixes** | Destination IP address prefixes excluded from port-scan detection. Use this for approved target ranges where scan-like behavior is expected. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ports** | Destination port numbers excluded from port-scan detection. | — | list of integer | — |

#### [Behavioral analytics — exclusions: ConnectionSprayExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-connectionsprayexclusions-sub-settings)

*Source/destination IP prefix and port exclusions for connection spray. Broadcast and multicast services (e.g. DNS on 53, mDNS on 5353, NetBIOS on 137/138) often appear as connection sprays in flat network segments because a single source contacts many hosts on the same well-known port.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from connection-spray detection. Use this for approved scanners, monitoring systems, or network services that contact many destinations. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ip Prefixes** | Destination IP address prefixes excluded from connection-spray detection. Use this for destination ranges where broad connection patterns are expected. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ports** | Destination port numbers excluded from connection-spray detection. | — | list of integer | — |

#### [Behavioral analytics — exclusions: FastFluxExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-fastfluxexclusions-sub-settings)

*Domain suffix exclusions for fast-flux DNS detection. Suffixes listed here represent known benign CDN, cloud, update, or SaaS domains that can legitimately rotate through many IP addresses with low TTLs. Downstream SQL should treat each suffix as normalized DNS text and match both the exact domain and any subdomain boundary; for example, google.com matches google.com and www.google.com but does not match notgoogle.com.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Domain Suffixes** | Normalized DNS domain suffixes excluded from fast-flux detection. Each entry should be a lowercase suffix such as 'google.com'. Downstream filters should match both the exact domain and subdomains on a label boundary (for example, 'google.com' matches 'google.com' and 'www.google.com', not 'notgoogle.com'). Do not include wildcard prefixes such as '*.' or SQL wildcards. Default: empty (no exclusions). | — | list of string | — |

#### [Behavioral analytics — exclusions: DGAExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-dgaexclusions-sub-settings)

*Source IP prefix, domain suffix, and TLD exclusions for DGA detection. Source exclusions suppress known benign resolvers or internal systems from DGA scoring. Suffix exclusions suppress known benign, noisy, or internal zones. TLD exclusions suppress the final DNS label when an entire private or noisy top-level zone is expected to generate high NXDOMAIN volumes.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from DGA detection. Use this for known benign resolvers, test systems, or internal services that generate noisy NXDOMAIN patterns. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Domain Suffixes** | Normalized DNS domain suffixes excluded from DGA detection. Use this for known benign, internal, or noisy zones where NXDOMAIN behavior should not contribute to DGA scoring. Downstream filters should match both the exact domain and subdomains on a label boundary. Do not include wildcard prefixes such as '*.' or SQL wildcards. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Tlds** | Normalized DNS top-level-domain labels excluded from DGA detection. Each entry should be a single final DNS label without a leading dot, such as 'local' or 'test'. Downstream filters should compare against the query name's final label only. Do not include wildcard or SQL wildcard characters. Default: empty (no exclusions). | — | list of string | — |

#### [Behavioral analytics — exclusions: DNSTunnelingExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-dnstunnelingexclusions-sub-settings)

*Domain suffix exclusions for DNS tunneling detection. Suffixes listed here represent benign, internal, or intentionally noisy domains where long labels, many subdomains, or large responses are expected and should not contribute to DNS tunneling alerts. Downstream SQL should match each suffix against the exact domain or a subdomain label boundary.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Domain Suffixes** | Normalized DNS domain suffixes excluded from DNS tunneling detection. Each entry should be a lowercase suffix such as 'corp.example'. Downstream filters should match both the exact domain and subdomains on a label boundary. Do not include wildcard prefixes such as '*.' or SQL wildcards. | — | list of string | — |
| **Excluded Registrable Domains** | Registrable domains (public-suffix eTLD+1) excluded from DNS tunneling detection as an exact equality key. Use this to suppress benign cloud-telemetry domains that generate long/random subdomains (for example 'amazonaws.com', 'azure.com', 'opinsights.azure.com'). Each entry must be a lowercase name of at least two labels; authoritative eTLD+1 canonicalization happens at enrichment. | — | list of string | — |
| **Excluded Answer Asns** | Autonomous-system numbers of the *answered* address excluded from DNS tunneling detection as an exact equality key. This targets the resolved destination, not the DNS resolver, so allowlisting a cloud provider ASN suppresses that provider's benign telemetry without blinding a whole resolver. Each entry must be a valid ASN (1–4294967295; reserved 0 and AS_TRANS 23456 are rejected). | — | list of integer | — |
| **Excluded Answer Countries** | ISO 3166-1 alpha-2 country codes of the *answered* address excluded from DNS tunneling detection as an exact equality key. Combined with per-sensor targeting this expresses region policy (for example a sensor in one region allowlisting a neighbouring country that a sensor elsewhere still flags). Codes are uppercased; unknown/user-assigned placeholders (ZZ, XX, ...) are rejected. | — | list of string | — |

#### [Behavioral analytics — exclusions: SuspiciousPortExclusions sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions#behavioral-analytics--exclusions-suspiciousportexclusions-sub-settings)

*Source/destination IP prefix and port exclusions for suspicious-port (protocol/port-mismatch) detection.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Excluded Source Ip Prefixes** | Source IP address prefixes excluded from suspicious-port detection. Use this for hosts that legitimately drive high-byte flows over non-standard ports. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ip Prefixes** | Destination IP address prefixes excluded from suspicious-port detection. Use this for approved targets where high-byte traffic on non-standard ports is expected. Each entry is matched as a SQL LIKE prefix; do not include a trailing '%'. Default: empty (no exclusions). | — | list of string | — |
| **Excluded Destination Ports** | Destination port numbers excluded from suspicious-port detection. | — | list of integer | — |

**Related:** [Behavioral detections](/docs/mdndr/operating-guide/behavioral-detections)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
