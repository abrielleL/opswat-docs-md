<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/behavioral-analytics-thresholds -->

# Behavioral analytics — thresholds

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → Behavioral analytics — thresholds

Tune the behavioral detections. Set the trigger and severity thresholds for each detection type.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Beaconing** | Operator-facing tunables for beaconing detection, including window size, candidate filters, severity bands, and confidence thresholds. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Data Exfiltration** | Operator-facing tunables for data exfiltration detection, covering aggregation windows, upload ratio filters, and severity bands. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Long Duration** | Operator-facing tunables for long-duration flow detection, including minimum duration and severity cutoffs. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Port Scan** | Operator-facing tunables for port scan detection, including window size and unique-port severity bands. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Connection Spray** | Operator-facing tunables for connection spray detection, including destination-count thresholds for each severity tier. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **DNS Tunneling** | Operator-facing tunables for DNS tunneling detection, including suspicious query characteristics and severity cutoffs. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Dga** | Operator-facing tunables for DGA detection, including query windowing and NXDOMAIN ratio thresholds. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Fast Flux** | Operator-facing tunables for fast-flux DNS detection, including unique-IP counts and TTL thresholds. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Suspicious Port** | Operator-facing tunables for suspicious-port / protocol-port mismatch detection, including window size, byte floor, and severity byte bands. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |

#### [Behavioral analytics — thresholds: BeaconingThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-beaconingthresholds-sub-settings)

*Thresholds for beaconing detection (4h HOP window).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for beaconing detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its window, thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Hours** | HOP window size for beaconing analysis. | `4` | number; 1 to 24; unit: hours | — |
| **Slow Tier Enabled** | Per-sensor opt-in for the FIXED 24h long-horizon beaconing tier. Default DISABLED: enabling the detector runs only the fast window; an operator must additionally opt a sensor into the slow tier to catch low-and-slow beacons (e.g. once per hour) that lack enough interval samples in the fast window. Kept off by default because the 24h horizon also surfaces benign periodic pollers (update checkers, telemetry, SaaS keepalives), so curate per-sensor destination allowlists before enabling. | Off | on/off | — |
| **Slow Window Hours** | HOP window size for the beaconing slow tier. FIXED deployment constant rendered into the pipeline SQL at image build (not live-tunable in Phase 2); changing it requires a pipeline restart/rebuild. Per-sensor / arbitrary live windows are deferred to Phase 3. | `24` | number; 6 to 168; unit: hours | — |
| **Min Connection Count** | Minimum connections to flag as candidate beacon. | `15` | number; 5 to 500 | — |
| **Max Stddev Bytes** | Maximum byte-size standard deviation (beacons have low variance). | `1000` | number; 100 to 100000; unit: bytes | — |
| **Critical Connection Count** | Connection count threshold for CRITICAL severity. | `50` | number; 10 to 1000 | — |
| **High Connection Count** | Connection count threshold for HIGH severity. | `30` | number; 10 to 1000 | — |
| **Medium Connection Count** | Connection count threshold for MEDIUM severity. | `20` | number; 5 to 500 | — |
| **High Confidence Stddev** | Stddev bytes below this → high confidence. | `100` | number; 10 to 10000 | — |
| **Medium Confidence Stddev** | Stddev bytes below this → medium confidence. | `500` | number; 10 to 50000 | — |
| **Max Jitter Cv** | Maximum inter-arrival jitter (coefficient of variation) for a non-IOC beacon. Lower = stricter periodicity requirement. Beacons have near-constant intervals (low jitter); noisy human traffic has high jitter and is excluded above this value. | `0.5` | number; 0.05 to 2.0 | — |
| **Emit Low Severity** | Emit LOW-severity beaconing detections (1) or suppress them (0). Suppressing LOW removes the highest-volume, lowest-value noise (monitoring agents / IoT phone-home) while keeping MEDIUM+. | `0` | number; 0 to 1 | — |
| **Max Response Packets** | Response-asymmetry threshold: the maximum number of server→client packets in the window for a beacon to count as UNANSWERED. This is the PRIMARY, jitter-independent beaconing signal — persistent outbound to a host that (almost) never replies is highly suspicious regardless of timing regularity, so a candidate qualifies on asymmetry alone even when its inter-arrival jitter is high. 0 = strictly silent peer (no reply packets); 1 (default) tolerates a single stray/RST-style packet. Raise to allow minimal ACK-style chatter. | `1` | number; 0 to 1000; unit: packets | — |
| **Min Request Packets** | Minimum client→server packets in the window for the response-asymmetry path to qualify a candidate. Filters trivial single-packet noise (a lone SYN, one-off UDP probe) so only genuinely persistent unanswered outbound escalates. Only applies to the asymmetric-beacon path; the classic regular-interval path is unaffected. | `2` | number; 1 to 1000000; unit: packets | — |
| **Min Unanswered Buckets** | Minimum number of distinct active hour-buckets (persistence gate) for the response-asymmetry path to qualify a candidate. Suspicion rises the more unanswered outbound is seen across time, so this requires the beacon to span at least N separate hours within the window — killing fire-and-forget bursts (a single noisy minute of one-way UDP) while surfacing low-and-slow C2 that persists. Bounded by the window size (fast tier ~4h, slow tier up to 168h). Only applies to the asymmetric path. | `3` | number; 1 to 168; unit: buckets | — |

#### [Behavioral analytics — thresholds: DataExfiltrationThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-dataexfiltrationthresholds-sub-settings)

*Thresholds for data exfiltration detection (15m HOP window).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for data-exfiltration detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its window, thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Minutes** | HOP window size for exfiltration analysis. | `15` | number; 5 to 60; unit: minutes | — |
| **Slow Tier Enabled** | Per-sensor opt-in for the FIXED 24h long-horizon data-exfiltration tier. Default DISABLED: enabling the detector runs only the fast window; opt a sensor into the slow tier to catch low-and-slow trickle exfiltration. Kept off by default because the long horizon also surfaces benign periodic traffic, so curate per-sensor destination allowlists before enabling. | Off | on/off | — |
| **Slow Window Hours** | HOP window size for the exfiltration slow tier. FIXED deployment constant rendered into the pipeline SQL at image build (not live-tunable in Phase 2). Per-sensor / arbitrary live windows are deferred to Phase 3. | `24` | number; 6 to 168; unit: hours | — |
| **Min Upload Ratio** | Minimum upload-to-download ratio to flag. | `2.0` | number; 1.0 to 100.0 | — |
| **Min Upload Bytes** | Minimum total upload bytes to flag (default 1 MB). | `1048576` | number; 1024 to 1073741824; unit: bytes | — |
| **Critical Upload Ratio** | Upload ratio threshold for CRITICAL severity. | `10.0` | number; 1.0 to 1000.0 | — |
| **Critical Upload Bytes** | Upload bytes threshold for CRITICAL severity (default 100 MB). | `104857600` | number; 1048576 to 1073741824; unit: bytes | — |
| **High Upload Ratio** | Upload ratio threshold for HIGH severity. | `5.0` | number; 1.0 to 500.0 | — |
| **High Upload Bytes** | Upload bytes threshold for HIGH severity (default 10 MB). | `10485760` | number; 1048576 to 1073741824; unit: bytes | — |
| **Emit Low Severity** | Emit LOW-severity data-exfiltration detections (1) or suppress them (0). Suppressing LOW removes everyday backup / cloud-sync / log-shipping noise while keeping MEDIUM+. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: LongDurationThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-longdurationthresholds-sub-settings)

*Thresholds for long-duration flow detection (per-event).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for long-duration flow detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its duration cutoffs, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Min Duration Seconds** | Minimum flow duration to flag (default 1 hour). | `3600` | number; 600 to 86400; unit: seconds | — |
| **Critical Duration Seconds** | Duration threshold for CRITICAL severity (default 24 hours). | `86400` | number; 3600 to 604800; unit: seconds | — |
| **High Duration Seconds** | Duration threshold for HIGH severity (default 10 hours). | `36000` | number; 3600 to 604800; unit: seconds | — |
| **Emit Low Severity** | Emit LOW-severity long-duration detections (1) or suppress them (0). Suppressing LOW keeps only flows that clear the HIGH duration floor. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: PortScanThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-portscanthresholds-sub-settings)

*Thresholds for port scan detection (1h HOP window).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for port-scan detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its window, thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Minutes** | HOP window size for port scan analysis. | `60` | number; 15 to 240; unit: minutes | — |
| **Min Unique Ports** | Minimum unique ports scanned to flag as candidate. | `10` | number; 3 to 1000 | — |
| **Critical Unique Ports** | Unique ports threshold for CRITICAL severity. | `100` | number; 10 to 10000 | — |
| **High Unique Ports** | Unique ports threshold for HIGH severity. | `50` | number; 10 to 5000 | — |
| **Medium Unique Ports** | Unique ports threshold for MEDIUM severity. | `20` | number; 5 to 1000 | — |
| **Emit Low Severity** | Emit LOW-severity port-scan detections (1) or suppress them (0). Suppressing LOW keeps only scans that clear the MEDIUM unique-port floor. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: ConnectionSprayThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-connectionspraythresholds-sub-settings)

*Thresholds for connection spray detection (1h HOP window).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for connection-spray detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its window, thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Minutes** | HOP window size for connection spray analysis. | `60` | number; 15 to 240; unit: minutes | — |
| **Min Unique Destinations** | Minimum unique destination IPs to flag as candidate. | `20` | number; 5 to 1000 | — |
| **Extreme Unique Destinations** | Unique destinations for extreme CRITICAL tier. | `200` | number; 50 to 50000 | — |
| **Critical Unique Destinations** | Unique destinations threshold for CRITICAL severity. | `100` | number; 10 to 10000 | — |
| **High Unique Destinations** | Unique destinations threshold for HIGH severity. | `50` | number; 10 to 5000 | — |
| **Emit Low Severity** | Emit LOW-severity connection-spray detections (1) or suppress them (0). Suppressing LOW keeps only sprays that clear the MEDIUM unique-destination floor. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: DNSTunnelingThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-dnstunnelingthresholds-sub-settings)

*Thresholds for DNS tunneling detection.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for DNS-tunneling detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its suspicion thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Long Query Length** | Query length above this flags as suspicious. | `60` | number; 10 to 500 | — |
| **Many Subdomains** | Subdomain count above this flags as suspicious. | `5` | number; 2 to 20 | — |
| **Large Response** | Answer length above this flags as suspicious. | `200` | number; 50 to 10000; unit: bytes | — |
| **Min Suspicion Score** | Minimum suspicion score required to emit a DNS tunneling candidate. | `2` | number; 1 to 10 | — |
| **High Suspicion Score** | Suspicion score for HIGH severity. | `3` | number; 1 to 10 | — |
| **Medium Suspicion Score** | Suspicion score for MEDIUM severity. | `2` | number; 1 to 10 | — |
| **Emit Low Severity** | Emit LOW-severity DNS-tunneling detections (1) or suppress them (0). Suppressing LOW removes the AV/cloud-DNS lookups that sit at the minimum suspicion score while keeping MEDIUM+. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: DGAThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-dgathresholds-sub-settings)

*Thresholds for DGA (Domain Generation Algorithm) detection.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for DGA detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its query windowing, NXDOMAIN-ratio thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Hours** | TUMBLE window size. | `1` | number; 1 to 24; unit: hours | — |
| **High Nxdomain Ratio** | NXDOMAIN ratio for HIGH severity. | `0.7` | number; 0.1 to 1.0 | — |
| **High Min Queries** | Min queries with high ratio for HIGH severity. | `50` | number; 5 to 10000 | — |
| **Medium Nxdomain Ratio** | NXDOMAIN ratio for MEDIUM severity / WHERE filter. | `0.5` | number; 0.1 to 1.0 | — |
| **Medium Min Queries** | Min queries with medium ratio for MEDIUM severity / WHERE filter. | `20` | number; 5 to 10000 | — |
| **Emit Low Severity** | Emit LOW-severity DGA (heuristic) detections (1) or suppress them (0). Suppressing LOW removes single-domain heuristic hits (browser random NXDOMAIN probes) while keeping MEDIUM+. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: FastFluxThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-fastfluxthresholds-sub-settings)

*Thresholds for fast flux DNS detection.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for fast-flux DNS detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its unique-IP / TTL thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Hours** | TUMBLE window size. | `1` | number; 1 to 24; unit: hours | — |
| **High Unique Ips** | Unique IPs for HIGH severity. | `10` | number; 3 to 1000 | — |
| **High Max Ttl** | Max TTL with unique IPs for HIGH severity. | `300` | number; 10 to 86400; unit: seconds | — |
| **Medium Unique Ips** | Unique IPs for MEDIUM severity / WHERE filter. | `5` | number; 2 to 500 | — |
| **Medium Max Ttl** | Max TTL with unique IPs for MEDIUM severity / WHERE filter. | `600` | number; 10 to 86400; unit: seconds | — |
| **Min Answer Asns** | Minimum distinct answer-IP ASNs required for a fast-flux MEDIUM/HIGH. CDNs resolve to many IPs across FEW ASNs; botnet fast-flux spans MANY ASNs. Raising this suppresses CDN false positives (fail-open when ASN enrichment is missing). | `2` | number; 1 to 100 | — |
| **Emit Low Severity** | Emit LOW-severity fast-flux detections (1) or suppress them (0). Suppressing LOW keeps only domains that clear the MEDIUM unique-IP / TTL floor. | `0` | number; 0 to 1 | — |

#### [Behavioral analytics — thresholds: SuspiciousPortThresholds sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds#behavioral-analytics--thresholds-suspiciousportthresholds-sub-settings)

*Thresholds for suspicious-port / protocol-port mismatch detection. Flags flows where the parsed application protocol contradicts the destination port's expected service (masquerade / tunnel), gated by the volume of data moved over the mismatched channel. Severity keys off the byte volume; a real tunnel moves data, stray probes do not.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Master switch for suspicious-port detection: enabled or disabled. Behavioral detectors ship DISABLED by default; an operator must explicitly enable this detector and review its window, byte thresholds, severity bands, and whitelist before it emits. A disabled detector produces no behavioral alerts. | Off | on/off | — |
| **Window Hours** | HOP window size for protocol-port mismatch aggregation. | `1` | number; 1 to 24; unit: hours | — |
| **Min Bytes** | Minimum bytes over the mismatched channel to flag (default 2 KB; drops stray probes). | `2048` | number; 0 to 1073741824; unit: bytes | — |
| **Medium Bytes** | Byte volume threshold for MEDIUM severity (default 4 KB). | `4096` | number; 0 to 1073741824; unit: bytes | — |
| **High Bytes** | Byte volume threshold for HIGH severity (default 64 KB). | `65536` | number; 0 to 1073741824; unit: bytes | — |
| **Critical Bytes** | Byte volume threshold for CRITICAL severity (default 1 MB). | `1048576` | number; 0 to 1073741824; unit: bytes | — |
| **Emit Low Severity** | Emit LOW-severity suspicious-port detections (1) or suppress them (0). Suppressing LOW keeps only mismatches that clear the MEDIUM byte floor. | `0` | number; 0 to 1 | — |

**Related:** [Behavioral detections](/docs/mdndr/operating-guide/behavioral-detections) · [ML anomaly detections](/docs/mdndr/operating-guide/ml-anomaly-detections)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
