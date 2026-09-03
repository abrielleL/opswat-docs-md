<!-- source: https://www.opswat.com/docs/mdndr/overview/overview -->

# Overview

## [What MetaDefender NDR does](/docs/mdndr/overview/overview#what-metadefender-ndr-does)

MetaDefender NDR is a network detection and response (NDR) platform. It turns mirrored network traffic into searchable security telemetry and clear alerts.

The sensor observes the traffic on the monitored network segments. The sensor decodes the protocols and rebuilds the sessions. The platform adds threat intelligence and file analysis verdicts to the metadata. The platform then applies three detection types: signature, behavioral, and machine-learning (ML). These detections find malicious activity, policy violations, and suspect communications. Operators use a central web interface to work with the alerts and the event history. Downstream systems receive the same data through syslog and integration APIs.

MetaDefender NDR is for security operations center (SOC) teams, network security engineers, and threat hunters. These users need deep visibility into east-west and north-south traffic. They need context-rich alerts. They need one place to pivot between flows, files, and entities during an investigation.

## [High-level architecture](/docs/mdndr/overview/overview#high-level-architecture)

MetaDefender NDR uses a distributed architecture. The architecture has one central Manager and one or more network sensors.

- **Manager.** The Manager is the central control and visibility plane. The Manager hosts the web user interface (UI). The Manager collects telemetry and alerts from all connected sensors. The Manager stores the enriched events and applies the detection policy. The Manager manages the users and the role-based access control (RBAC). The Manager owns the integrations with external systems. An administrator configures the global policy and the per-sensor policy from the Manager. An analyst triages the alerts, hunts, and investigates from the Manager.
- **Sensors.** A sensor is a traffic-inspection point. You deploy a sensor at a network vantage location. Each sensor connects to a network tap, a switched port analyzer (SPAN) port, or a virtual network interface. The sensor receives the mirrored traffic. The sensor parses the protocols, rebuilds the sessions, and extracts the files. The sensor then sends the metadata and the carved files to the Manager. The Manager does the enrichment, the correlation, and the storage. Sensors scale horizontally. You can deploy more sensors close to the critical segments, and you do not restructure the Manager.

A deployment can be small or large. A small deployment has one Manager and one co-located sensor, for a small site or an evaluation. A large deployment has one Manager and many distributed sensors, for an enterprise or a managed security service provider (MSSP).

## [How the platform processes traffic](/docs/mdndr/overview/overview#how-the-platform-processes-traffic)

Each network event moves through a multi-stage pipeline. The pipeline changes raw packets into enriched, searchable records.

1. **Capture and parse.** The sensor receives the mirrored traffic. The sensor rebuilds the sessions and decodes the application protocols, for example HTTP, TLS, DNS, and SMB. The sensor extracts the per-transaction metadata and the carved files.
2. **Enrichment.** The platform adds context to the metadata. The context includes command-and-control (C2) indicator matches, InSights Threat Intelligence DB (TIDB) and Reputation DB (REPDB) hits, and Autonomous System Number (ASN) and GeoIP lookups. For a carved file, the context also includes the MetaDefender Core scan result.
3. **Aggregation.** The platform stitches each enrichment back onto the original event. A downstream consumer then sees one fully-enriched record, not a stream of fragments.
4. **Detection and storage.** The platform evaluates the enriched record against the Suricata signatures, the behavioral detections, the ML anomaly models, and the alert rules. The Manager stores the events and the alerts in long-term storage. The Manager makes them available for search, drill-down, and export.
5. **Presentation.** The Manager shows live and historical data. The Dashboard gives an overview and trends. The Hunt page gives search, pivot, and drill-down. The detail panes link an alert back to its flow, file, and entity context.

The pipeline runs in near real time. An alert usually appears in the Manager within seconds of the observed traffic.

## [Deployment models](/docs/mdndr/overview/overview#deployment-models)

MetaDefender NDR supports several deployment models. You can align the platform with your infrastructure, your data-residency rules, and your operational preferences.

- **On-premises appliance.** You install the Manager and the sensors on dedicated physical hardware. Use this model for production with strict data-residency, performance, or isolation rules.
- **Virtual appliance.** You install the Manager and the sensors as virtual machines in an on-premises hypervisor. Use this model for an evaluation, a lab, a small site, or consolidated virtual infrastructure.
- **Cloud-hosted and hybrid.** You deploy sensors in a cloud environment to monitor cloud network traffic. The sensors connect back to a central Manager. A hybrid deployment combines on-premises sensors and cloud sensors under one Manager. You then monitor distributed sites from one console.

## [Integration points](/docs/mdndr/overview/overview#integration-points)

MetaDefender NDR fits into your existing security tools. It does not replace them. The platform gives these integration points:

- **SIEM through syslog.** The platform forwards alerts and selected events to one or more security information and event management (SIEM) systems over syslog. You configure the destinations. A group-level filter sends only the relevant alerts to a given SIEM.
- **MetaDefender Core.** The platform integrates with MetaDefender Core for deep analysis of traffic-carved files. MetaDefender Core scans each file with many engines and adds a verdict. The platform stitches the scan result back onto the original event. The result drives the MetaDefender Core file-scanning detection family.
- **MetaDefender Sandbox.** You can submit selected files for dynamic analysis. The Sandbox identifies evasive or unknown threats. The platform returns the result as extra context on the event.
- **Directory services.** The platform integrates with enterprise identity stores, for example Lightweight Directory Access Protocol (LDAP) and Active Directory (AD). The platform uses these stores for central authentication and RBAC mapping. You reuse your existing group membership to control platform access.

## [Further reading](/docs/mdndr/overview/overview#further-reading)

- [Overview](/docs/mdndr/operating-guide/analyst-overview) — a longer treatment of the concepts, capabilities, and architecture.
- [Dashboard](/docs/mdndr/operating-guide/dashboard) — the analyst home surface.
- [Hunt page](/docs/mdndr/operating-guide/hunt-page) — search, pivot, and drill-down across the enriched telemetry.
