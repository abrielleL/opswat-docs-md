<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/ip-enrichment -->

# IP enrichment

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → IP enrichment

Add geographic and network owner data to Internet Protocol (IP) addresses in alerts and flows.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Enable the IP enrichment service. | On | on/off | — |
| **Data Path** | Directory containing the IP2Location databases (GeoIP DB11 + LITE-ASN .BIN files). | `/etc/ndr/ip` | text | Restart needed |
| **Default Home Net** | Fallback CIDR ranges treated as internal/'home' networks by this service when the originating sensor has no per-sensor `sensor.home_net` configured (e.g. before sensor registration completes). Used to classify per-IP locality (internal vs external) and to derive the event-level traffic_direction. Defaults to the RFC1918 private ranges. | `["192.168.0.0/16", "10.0.0.0/8", "172.16.0.0/12"]` | list of string | Restart needed |

**Related:** [C2 and threat intelligence](/docs/mdndr/operating-guide/c2-and-threat-intelligence)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
