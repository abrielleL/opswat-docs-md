<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/severity-and-confidence -->

# Severity and Confidence

Every alert MetaDefender NDR produces carries two numbers. A **severity label** comes from a unified four-level scale. A **confidence score** is a floating-point value between 0.40 and 0.99. Together, they define the urgency and the detection trust level. Analysts use severity to pick *what to look at next*. They use confidence to order work *within* a severity band. All detection families use the same vocabulary. These families include Suricata signatures, command-and-control (C2) intelligence, OPSWAT InSights threat intelligence, MetaDefender Core file scan, behavioral analytics, and machine-learning (ML) anomaly detection.

This chapter defines the scales. It documents indicator-of-compromise (IOC) auto-escalation, which can override them. It explains how severity changes the user interface (UI). It also states the platform stance on service-level agreements (SLAs).

Acronyms expanded in this chapter:

- IOC: Indicator of Compromise.
- SLA: service-level agreement.
- C2: command-and-control.
- UI: user interface.
- ML: machine learning.
- RCF: Random Cut Forest.
- AV: antivirus.
- TIDB: Threat Intelligence Database.
- REPDB: Reputation Database.
- IDS: intrusion detection system.

## [The unified severity scale](/docs/mdndr/operating-guide/severity-and-confidence#the-unified-severity-scale)

MetaDefender NDR classifies every alert into one of four severity levels. The alert engine sets the level when the rule fires. It uses the native trigger conditions of the detection.

| Severity | Operational meaning | Typical trigger |
| --- | --- | --- |
| **Critical** | Confirmed threat or extreme anomaly. The alert names a known-bad indicator, crosses the highest detection threshold, or carries a Suricata signature marked Critical. Analysts stop other work and triage. | An IOC match on any entity in the event. A beaconing detection has 50 or more connections in the 4-hour window. A scanned file has 6 or more positive antivirus engines. A Suricata rule has native severity 1. |
| **High** | Strong indicator of malicious activity. The evidence is compelling but not yet conclusive. Analysts start triage at the top of the queue after Critical is drained. | An InSights TIDB-only match. A beaconing window has 30 or more connections. A file has 3 to 5 positive antivirus engines. A Suricata rule has native severity 2. |
| **Medium** | Moderate anomaly that warrants investigation but is not individually alarming. Triage follows after Critical and High. | An InSights REPDB-only match without a TIDB hit. A beaconing window has 20 or more connections. An ML anomaly pass-through finding. A Suricata rule has native severity 3. |
| **Low** | Mild anomaly or informational finding. Meets the minimum threshold for the detection but may well be benign. Analysts review in batch, not individually. | The lowest trigger of a behavioral detection. For example, a beaconing window has 15 connections. A MetaDefender Core match has 1 to 2 positive antivirus engines. A Suricata rule has native severity 4. Policy-violation signatures. |

The scale is absolute, not relative to the deployment. A Critical alert at a small single-sensor installation has the same meaning as one at a large multi-sensor fleet. The detection pipeline fixes the thresholds that produce each label. They are identical across every site.

Severity has no built-in decay. A Critical alert remains Critical until an analyst closes it. The platform does not automatically demote it as time passes. Analysts manage state through the Hunt page and runbook workflows in [Daily Operations](/docs/mdndr/operating-guide/daily-operations).

## [The confidence score range](/docs/mdndr/operating-guide/severity-and-confidence#the-confidence-score-range)

Alongside severity, every alert carries a confidence score. Confidence is a floating-point number on the closed interval **0.40** to **0.99**. It quantifies the detection engine's trust in its own finding. It shows how likely it is that the alert represents real malicious or anomalous activity rather than noise.

| Band | Range | meaning |
| --- | --- | --- |
| **Very high** | 0.95-0.99 | IOC match or extreme observed values. The detection tells the analyst *this is really bad*. The evidence is overwhelming. |
| **High** | 0.80-0.94 | Strong behavioral signal with corroborating evidence. The detection has crossed a major threshold and the secondary indicators align. |
| **Moderate** | 0.60-0.79 | A clear behavioral anomaly is present, but it warrants context before escalation. The detection has enough evidence to fire but benefits from analyst review. |
| **Low** | 0.40-0.59 | Meets the minimum detection threshold but may be benign. Expect a higher false-positive rate in this band. |

The platform emits no alert below 0.40. It filters out signals that do not clear the minimum-confidence floor. The top of the band is 0.99, not 1.00. Thus, "perfect confidence" stays reserved for the IOC auto-escalation pathway below.

Analysts use confidence to order work **within** a severity band. Among ten Medium alerts, triage the alert at 0.78 confidence before the alert at 0.42. Analysts never use confidence **across** severity bands. A Medium at 0.94 is still less urgent than a High at 0.40.

## [Suricata native severity](/docs/mdndr/operating-guide/severity-and-confidence#suricata-native-severity)

Suricata is the intrusion detection system (IDS) engine inside every MetaDefender NDR sensor. It assigns rules their own severity on a **1 to 4** scale. The rule author sets the scale value. The convention is inverted relative to many other security tools. A **lower** number means a **more severe** rule.

| Suricata value | Suricata Level | MetaDefender NDR Severity |
| --- | --- | --- |
| **1** | Critical | Critical |
| **2** | High | High |
| **3** | Medium | Medium |
| **4** | Low | Low |

The alert engine applies this mapping one-to-one when a Suricata signature fires. Analysts see the native number in the raw `alert.severity` value. This value appears on a Suricata alert row in the Hunt page sidebar, in the *Suricata Alert + Payload* section. The separate *Severity* column on the row shows the mapped unified label. The two values should always agree for signature alerts. Report a mismatch as a bad rule-severity mapping.

The inversion trap is the most common source of confusion for analysts from other platforms. In those platforms, "severity 5" can mean critical. A Suricata rule set to severity 1 is **not** low. It is Critical. When you author or import custom Suricata rules, mirror the Proofpoint Emerging Threats convention. Reserve 1 for confirmed attack signatures. Reserve 2 for likely malicious activity. Reserve 3 for potentially unwanted activity. Reserve 4 for informational or policy-only rules.

## [IOC auto-escalation rule](/docs/mdndr/operating-guide/severity-and-confidence#ioc-auto-escalation-rule)

A single, non-negotiable rule overrides the native severity and confidence whenever an IOC match is present on an event:

> **If any entity on an event matches the C2 feed or the InSights TIDB or REPDB feeds, the alert changes to Critical severity and 0.99 confidence. This rule applies regardless of the detection family's normal thresholds. It also applies regardless of what the native evidence alone would have produced.**

This rule applies to every detection family that can carry an IOC reference. It applies to behavioral detections whose destination is on the C2 feed. It applies to Suricata signature alerts whose source or destination matches InSights. It applies to MetaDefender Core alerts whose file moved to an IOC-listed endpoint. It applies to ML anomaly alerts whose entity is on a watchlist. The alert engine implements the rule internally. It uses the enriched-event field `insights.malicious_count > 0`. Operators and administrators cannot tune the rule.

The rule exists because the evidence changes category when it involves a known-bad indicator. A beaconing pattern might be polling. Polling *to a known command-and-control server* is no longer ambiguous. The signal is too strong to demote.

Two practical consequences:

- **Threshold-Critical vs IOC-Critical.** Analysts must know why a Critical alert is Critical. The label can come from the native threshold, for example 50 or more beaconing connections. It can also come from the IOC override, with any count to an IOC-listed destination. The Hunt page sidebar shows the distinction. An IOC-Critical alert renders a *C2 Enrichment* or *InSights Enrichment* section. That section names the matched entity and the source feed. A threshold-Critical alert carries only the family-native metadata. Treat IOC-Critical alerts as the stronger signal. Native evidence plus a confirmed indicator is worse than native evidence alone.
- **A Low behavioral alert can become Critical.** A Long Duration Flow of 3,700 seconds to a REPDB-listed domain normally lands as Medium. That is the pure-duration threshold tier. The REPDB hit pushes it to Critical at 0.99 confidence. Similarly, 15 beaconing connections become Critical if the destination is on the C2 feed. Do not dismiss IOC-escalated alerts because the underlying behavioral evidence looks modest. The escalation is the signal.

## [How severity changes the UI](/docs/mdndr/operating-guide/severity-and-confidence#how-severity-changes-the-ui)

Severity is a first-class visual channel on every operator surface.

- **Dashboard -- Recent Severities donut.** The donut chart segments recent alerts by Critical, High, Medium, Low, and Unknown. Operators use the donut as the fastest way to see the *shape* of the current alert stream: a sudden Critical spike is visually obvious.
- **Dashboard -- Recent Alerts widget.** Each alert row shows its severity as a colored label. The color cue lets operators scan the widget for Criticals without reading the column explicitly.
- **Hunt page -- severity column.** Every alert sub-tab exposes severity as a sortable, filterable first-class column. Analysts routinely sort the *All Alerts* tab by severity descending to work the highest-urgency items first.
- **Hunt page -- row urgency cues.** Row-level visual treatment, such as color coding and icon weight, reflects severity. Thus, a Critical row draws attention even when the severity column is out of view.
- **Hunt page -- detail sidebar.** When an analyst selects an alert row, the sidebar header shows the severity label and confidence score together. Enrichment sections that triggered IOC auto-escalation render prominently in the sidebar. Examples include *C2 Enrichment* and *InSights Enrichment*. The reason for the Critical label is one scroll away.

MetaDefender NDR does not use severity as a dashboard-wide filter on MVP. The current Dashboard interval filter is historical interval only. Severity-based cross-widget filters are on the Dashboard roadmap. Operators who must narrow the global view by severity use the [Hunt page](/docs/mdndr/operating-guide/hunt-page). It exposes the full filter grammar.

## [No SLA mapping in this guide](/docs/mdndr/operating-guide/severity-and-confidence#no-sla-mapping-in-this-guide)

MetaDefender NDR deliberately does not publish response-time SLAs keyed to severity. The platform provides the triage signal. The label says *this alert is more urgent than that one*. The operating organization's incident-response policy owns time-to-acknowledge, time-to-contain, and time-to-resolve targets.

The rationale is straightforward. The right SLA for a Critical alert depends on factors the platform cannot know. Examples include the shift coverage model, analyst headcount, and asset criticality at the alerting entity. Other factors include regulatory exposure, downstream automation coupling, and the deployment model. The deployment can be a Managed Security Service Provider (MSSP) multi-tenant environment. It can also be a direct enterprise Security Operations Center (SOC). A 15-minute time-to-acknowledge target can be reasonable for a direct-enterprise SOC on its crown-jewel subnet. The same target can be unreasonable for an MSSP that serves 200 customers with a tier-one team. The reverse can also be true.

Operators who must express SLAs in their own documentation should layer them over the platform severity scale. Example: *Critical: 15-minute acknowledge / 1-hour contain / 4-hour resolve; High: 1-hour / 4-hour / next business day; Medium and Low: best-effort*. Treat the severity label as the *input* to the SLA computation. Do not expect the platform to enforce deadlines. The alert engine does not escalate, reassign, or page on its own. Analysts manage all alert lifecycle actions on the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). [Daily Operations](/docs/mdndr/operating-guide/daily-operations) documents those actions.

For the end-to-end investigative workflow that starts from a Critical alert, see [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage). For the full catalog of detections and the severity range each produces before IOC auto-escalation.
