<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/behavioral-analytics-services -->

# Behavioral analytics — services

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → Behavioral analytics — services

Identify infrastructure services, such as internal resolvers, so the analytics engine treats their traffic correctly.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Infrastructure Services** | Catalog of periodic-by-design infrastructure services, keyed by destination port. Beaconing suppresses genuine matches (even when app_proto is unparsed); the protocol/port-mismatch detector escalates flows that contradict the expected transport/app_proto. Defaults ship the standard set (DNS, mDNS, LLMNR, NTP, NetBIOS, DHCP); per-sensor entries are additive to the global catalog. This is a group of settings. See the sub-settings below. | `[{"name": "dns", "ports": [53], "transport": "any", "expected_app_protos": ["dns"]}, {"name": "mdns", "ports": [5353], "transport": "udp", "expected_app_protos": ["dns"]}, {"name": "llmnr", "ports": [5355], "transport": "udp", "expected_app_protos": ["dns"]}, {"name": "ntp", "ports": [123], "transport": "udp", "expected_app_protos": ["ntp"]}, {"name": "netbios-ns", "ports": [137], "transport": "udp", "expected_app_protos": []}, {"name": "netbios-dgm", "ports": [138], "transport": "udp", "expected_app_protos": []}, {"name": "dhcp", "ports": [67, 68], "transport": "udp", "expected_app_protos": ["dhcp"]}]` | list of groups | — |

#### [Behavioral analytics — services: InfrastructureService sub-settings](/docs/mdndr/configuration-guide/behavioral-analytics-services#behavioral-analytics--services-infrastructureservice-sub-settings)

*A periodic-by-design network service keyed by destination port(s). An entry declares the ports a well-known infrastructure service listens on, the transport it is expected to use, and the Suricata app_proto tokens that legitimately appear for it. Detectors use this to (a) suppress genuine infrastructure traffic from beaconing even when app_proto is unparsed, and (b) flag traffic that contradicts the expected profile (protocol/port mismatch).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Name** | Friendly service name (e.g. 'dns', 'ntp', 'mdns'). Informational label carried on detections; matching is by port/transport/app_proto, not by this name. | — | text; up to 64 characters | — |
| **Ports** | Destination port(s) this service listens on. Each must be a valid TCP/UDP port (1–65535). | — | list of integer | — |
| **Transport** | Expected L4 transport for this service: 'udp', 'tcp', or 'any'. A flow whose transport contradicts a udp-only/tcp-only service is a protocol/port-mismatch signal. | `any` | text | — |
| **Expected App Protos** | Suricata app_proto tokens (lowercase) that legitimately appear on these ports (e.g. ['dns']). A flow to one of these ports whose PARSED app_proto is not in this list (and not blank) is treated as a masquerade/tunnel by the protocol/port-mismatch detector. Leave empty for services Suricata does not app-parse (e.g. NetBIOS). | — | list of string | — |

**Related:** [Behavioral detections](/docs/mdndr/operating-guide/behavioral-detections)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
