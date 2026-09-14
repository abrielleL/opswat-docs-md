<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/rcf-streaming -->

# RCF streaming

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → RCF streaming

Control the machine learning (ML) anomaly detection stream. The Random Cut Forest (RCF) engine scores traffic for anomalies.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Enable this service. | On | on/off | — |
| **Whitelist Enabled** | Enable whitelist checks. | On | on/off | — |
| **Directions** | Traffic directions to build per-(sensor,direction,protocol) RCF models for. Includes UNKNOWN so events whose endpoint locality cannot be resolved are still modeled rather than dropped by the early direction filter. | `["internal_to_external", "external_to_internal", "unknown"]` | `internal_to_internal`, `internal_to_external`, `external_to_internal`, `external_to_external`, `unknown` | Restart needed |
| **Flow** | Flow RCF profile. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Http** | HTTP RCF profile. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **DNS** | DNS RCF profile. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **TLS** | TLS RCF profile. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | Restart needed |
| **Critical Score** | Anomaly score at or above which a detection is mapped to CRITICAL severity (SeverityLevel.CRITICAL). On the canonical score scale (see the class docstring) the observed maximum is ~7, so this tier is deliberately reserved for extreme outliers. | `5` | number; 1 to 10000 | — |
| **High Score** | Anomaly score at or above which a detection is mapped to HIGH severity (below critical_score). | `4` | number; 1 to 10000 | — |
| **Medium Score** | Anomaly score at or above which a detection is mapped to MEDIUM severity (below high_score); scores below this map to LOW. Must sit at or above the per-protocol anomaly_threshold values, or no alert can ever be LOW. | `3` | number; 1 to 10000 | — |
| **Max Models** | Hard cap on total live RCF models (sensors x directions x protocols) for memory safety. | `10000` | number; 1 to 1000000 | — |

#### [RCF streaming: RCFProtocolProfile sub-settings](/docs/mdndr/configuration-guide/rcf-streaming#rcf-streaming-rcfprotocolprofile-sub-settings)

*Per-protocol RCF config contract. The top-level num_trees/shingle_size/tree_size/anomaly_threshold fields are the active (operator-facing default) tunables and are the MEDIUM sensitivity tier. The flat low_* and high_* fields carry the LOW and HIGH tiers so the streaming service can look up the parameters for any sensitivity preset entirely from the ontology with no hardcoded fallback.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Enable RCF for this protocol. | On | on/off | — |
| **Sensitivity** | Sensitivity preset for this protocol. | `medium` | `low`, `medium`, `high` | — |
| **Num Trees** | Number of trees in the RCF forest for this protocol. | `20` | number; 5 to 100 | — |
| **Shingle Size** | Shingle size (sequence length) for this protocol. | `3` | number; 1 to 16 | — |
| **Tree Size** | Maximum samples per tree for this protocol. | `128` | number; 32 to 1024 | — |
| **Training Min Samples** | Min data points this protocol's model must ingest before it exits training and begins alerting; 0 disables the gate (model alerts as soon as the forest window fills). | `100000` | number; 0 to 100000000 | — |
| **Anomaly Threshold** | Anomaly score cutoff for this protocol, on the native-backend score scale where ~1.0 is the expected score for in-distribution traffic (see RCFStreamingServiceConfig for the measured per-protocol distributions). A value drawn from a different backend's scale will silently never fire. | `2.5` | number; 0.5 to 100.0 | — |
| **Low Num Trees** | Number of trees in the RCF forest when this protocol runs at LOW sensitivity. | `20` | number; 5 to 100 | — |
| **Low Shingle Size** | Shingle size (sequence length) when this protocol runs at LOW sensitivity. | `3` | number; 1 to 16 | — |
| **Low Tree Size** | Maximum samples per tree when this protocol runs at LOW sensitivity. | `128` | number; 32 to 1024 | — |
| **Low Anomaly Threshold** | Anomaly score cutoff when this protocol runs at LOW sensitivity (native-backend scale; LOW sensitivity means FEWER alerts, so this sits ABOVE anomaly_threshold). | `3.0` | number; 0.5 to 100.0 | — |
| **High Num Trees** | Number of trees in the RCF forest when this protocol runs at HIGH sensitivity. | `20` | number; 5 to 100 | — |
| **High Shingle Size** | Shingle size (sequence length) when this protocol runs at HIGH sensitivity. | `3` | number; 1 to 16 | — |
| **High Tree Size** | Maximum samples per tree when this protocol runs at HIGH sensitivity. | `128` | number; 32 to 1024 | — |
| **High Anomaly Threshold** | Anomaly score cutoff when this protocol runs at HIGH sensitivity (native-backend scale; HIGH sensitivity means MORE alerts, so this sits BELOW anomaly_threshold). | `1.8` | number; 0.5 to 100.0 | — |

**Related:** [ML anomaly detections](/docs/mdndr/operating-guide/ml-anomaly-detections)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
