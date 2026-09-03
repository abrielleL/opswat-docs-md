<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/investigation-runbooks -->

# Investigation Runbooks

This chapter introduces the investigation runbooks that follow. Each runbook gives a step-by-step procedure. It takes an analyst from *"an alert has appeared"* to *"a triage decision has been recorded"*. The analyst uses the [Hunt Page](/docs/mdndr/operating-guide/hunt-page), the [Dashboard](/docs/mdndr/operating-guide/dashboard), and [Detection Overview](/docs/mdndr/operating-guide/detection-overview).

This chapter is for Tier 1 Security Operations Center (SOC) analysts who perform first-response triage. It is also for Tier 2 and Tier 3 analysts who escalate and resolve incidents. Threat hunters use it for proactive campaigns. Managed Security Service Provider (MSSP) analysts use it across customer tenants. SOC leads use it to maintain detection quality. It assumes familiarity with the Hunt page workspace and the six detection families.

First-use acronym expansions in this chapter:

- SOC: Security Operations Center.
- MSSP: Managed Security Service Provider.
- IOC: Indicator of Compromise.
- C2: command-and-control.
- PCAP: packet capture.
- TLS: Transport Layer Security.
- SNI: Server Name Indication.
- DNS: Domain Name System.
- IP: Internet Protocol.
- RCF: Random Cut Forest.
- AV: antivirus.
- PCR: Producer-Consumer Ratio.
- TIDB: Threat Intelligence Database.
- SLA: Service-Level Agreement.

## [Purpose of the runbooks](/docs/mdndr/operating-guide/investigation-runbooks#purpose-of-the-runbooks)

The runbooks exist to make triage repeatable. A runbook captures the observations for a specific trigger. It lists the pivots and filters that support those observations. It gives criteria for escalation, monitor, and closure decisions. It also lists false-positive patterns that recur across deployments.

Runbooks serve three audiences at once. Junior analysts follow them linearly as a checklist. Senior analysts skim them as a reminder of the pivots available on the Hunt page and the enrichment fields worth checking. SOC leads cite them in peer reviews and in incident post-mortems to explain why a given triage decision was or was not defensible.

Runbooks do not replace judgment. They list the evidence that an analyst must collect. They also list the questions that each evidence item answers. The final decision depends on the local environment, the threat landscape, and the context of the alerting host. Runbooks do not define response-time Service-Level Agreements (SLAs). Those agreements belong to the SOC's operating plan, not to product documentation. A runbook defines the operation order that supports a decision.

## [How to use a runbook](/docs/mdndr/operating-guide/investigation-runbooks#how-to-use-a-runbook)

Every runbook in this chapter follows a fixed shape. Read it in order to move from zero context to a documented triage outcome.

1. **Read the trigger scenario.** Read what the analyst sees on a Dashboard widget or Hunt tab. If the observed alert does not match the scenario, use a different runbook. If no family-specific runbook fits, use [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage).
2. **Check prerequisites.** Confirm the analyst has an open Hunt page session with an appropriate role. Confirm access to the detection family's sub-tab. Confirm any enrichment configuration that the runbook needs. If a prerequisite is absent, stop the investigation. Continue only after the gap is closed.
3. **Execute the investigation steps in order.** Follow the numbered steps in sequence. Each step gives one action and one result to examine. Do not skip steps when the answer looks obvious. Each step adds a distinct piece of evidence.
4. **Apply the decision tree.** Select one branch: escalate, monitor, close as benign, or tune the rule through policy. Record the minimum artifacts for the selected branch. Examples include a ticket identifier, a Hunt tab reference, or a policy change note.
5. **Review false-positive patterns.** Read the "Common False Positives" section. Use it to identify benign behaviors that recur for each detection family.
6. **Follow the references.** Use the cross-links for background and related runbooks. Use glossary entries for unfamiliar terms.

Analysts document the runbook name in the incident ticket. If the runbook is insufficient, the analyst files a note against it. The note can describe ambiguous evidence. It can describe a decision tree that did not terminate cleanly. It can describe a missing false-positive pattern. The next revision captures the gap.

## [Investigation mindset](/docs/mdndr/operating-guide/investigation-runbooks#investigation-mindset)

Every runbook shares a stance. It is worth naming the stance explicitly because it is the single most important thing a new analyst carries from runbook to runbook.

- **Collect evidence before action.** An alert is a hypothesis, not a conclusion. Before an analyst isolates a host, blocks an indicator, or closes a ticket, the analyst examines the row fields. The analyst examines the enrichment sidebar. The analyst also examines at least one correlated view. Examples include the same source IP, destination, flow, or file hash. The time cost is low. The cost of action on a misread alert is high.
- **Correlate across detection families.** A single-signal alert rarely justifies a major response. Multi-signal convergence is a stronger basis for escalation than any signal alone. One example is a behavioral beaconing detection with a C2 enrichment match. It is stronger when an OPSWAT InSights Threat Intelligence Database (TIDB) hit matches the same destination. Every runbook's decision tree weights confirmed correlation over isolated signals.
- **Never act on a single signal.** This is the operational expression of the previous two points. If the only evidence is one row on one tab, choose *monitor*. Do not choose *close* or *escalate* without enrichments, correlated events, or prior history. The analyst widens the search window. The analyst pivots to related surfaces. The analyst waits for a second signal before an action that is costly to reverse.
- **Record observations, not assumptions.** If an analyst closes a ticket as benign, the ticket note captures the fields that support that conclusion. Example: *"destination is 52.84.0.0/15, Amazon Web Services (AWS) CloudFront range, confirmed by Autonomous System Number (ASN) enrichment; user agent matches internal software update client; closing as benign"*. Later readers reopen the conclusion only if one of those fields changes. The team's rate of re-alerts on known-benign patterns drops.
- **Tune sparingly and deliberately.** Close as benign is a triage outcome. Rule tuning is a detection-engineering outcome. It removes future visibility into the same pattern. Runbooks separate the two outcomes. Tune when the same benign pattern has confirmation multiple times. Tune when the source of the noise is understood. Tune when a policy mechanism can exclude the pattern without true-positive loss. The rest of the time, set the disposition to *close as benign*. Keep the rule live.

## [Pivot patterns in runbooks](/docs/mdndr/operating-guide/investigation-runbooks#pivot-patterns-in-runbooks)

Every runbook uses the same pivots through the Hunt page. The [Hunt Page](/docs/mdndr/operating-guide/hunt-page) chapter describes the pivots in detail. The [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) meta-runbook also describes them. The overview here reminds you what each pivot does.

- **Alert → flow.** From an alert row, the analyst right-clicks the `community_id` column (or the matching field in the sidebar) and selects *Show all events with this community id*. A new *All Events* tab opens with every protocol transaction, flow record, file extraction, and enrichment that belongs to the same connection. This is the single most frequent pivot in triage.
- **Alert → session.** From an alert row, the analyst right-clicks the `community_id`. The analyst selects *Show related events*. The analyst then narrows the tab to a protocol-specific sub-tab. Examples include DNS, HTTP, TLS, Secure Shell (SSH), Server Message Block (SMB), Remote Desktop Protocol (RDP), Simple Mail Transfer Protocol (SMTP), File Transfer Protocol (FTP), Quick User Datagram Protocol Internet Connection (QUIC), and FileInfo. Use this pivot to inspect the payload metadata for that connection.
- **Alert → hunt by value.** Right-click an IP, domain, hash, or `community_id` value in the row or sidebar. The menu exposes *Hunt all events from this IP*, *Search file hash across all events*, or *Show related files*. Each action opens a new tab filtered to the pivot value. The tab preserves the current time range so history stays available.
- **Flow → session → file.** Pivot a long-duration or high-volume flow to its session records. If a session carries file metadata, pivot it to the *Files* bucket. Retrieve the extracted file and its MetaDefender Core scan result if present.
- **Session → PCAP.** When session metadata alone does not resolve the question, the analyst requests a packet capture (PCAP) for the flow's time window. PCAP availability is configuration-dependent and selective — not every flow has a PCAP retained. The runbook calls out when PCAP is the right pivot and when the analyst should stop at session metadata.
- **Value → hunt.** This is the simplest pivot. Right-click any IP, domain, or hash value. Select the matching *Hunt* action to produce a value-scoped tab. Analysts use it to check whether an indicator fired before. Analysts also use it to count occurrences over a longer window. They use it to find other hosts that interact with the same destination.

Pivots always open new tabs. The Hunt page preserves the originating tab. Thus, the analyst can return to the lead after the pivot. Tab persistence keeps the investigation state across sign-out and sign-in. Thus, runbooks can direct the analyst to close a loop later without prior context loss.

## [Runbook catalog](/docs/mdndr/operating-guide/investigation-runbooks#runbook-catalog)

Each entry below links to the corresponding runbook and names the detection family it covers. The time budget is a *typical* target for first-response triage on a single alert — more complex investigations routinely take longer and branch into incident response.

| Runbook | Trigger | Detection Family | Time Budget |
| --- | --- | --- | --- |
| [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) | Any Critical-severity alert on the Recent Alerts Dashboard widget or the *All Alerts* Hunt tab | Any | 10–15 min |
| [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) | Beaconing Detection or C2 Infrastructure Alert on a Hunt *All Alerts* tab | Behavioral beaconing, C2 threat intelligence | 15–25 min |
| [Data Exfiltration Investigation](/docs/mdndr/operating-guide/data-exfiltration-investigation) | Data Exfiltration Alert, or an unusually high upload ratio surfaced on the Producer-Consumer Ratio (PCR) Dashboard widget | Behavioral data exfiltration | 20–30 min |
| [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation) | MetaDefender Core High, Medium, or Low antivirus (AV) Detection alert | MetaDefender Core file scanning | 20–30 min |
| [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) | ML Random Cut Forest (RCF) Anomalous Activity Alert on a Hunt *All Alerts* tab | ML anomaly detection | 15–25 min |
| [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation) | DNS Tunneling Detection alert (per-query suspicion) or the DNS Tunneling Hourly aggregation alert | Behavioral tunneling | 15–20 min |
| [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) | Referenced from every other runbook as the pivot-mechanics meta-runbook | Cross-family | As needed |

## [See also](/docs/mdndr/operating-guide/investigation-runbooks#see-also)

- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) — the investigation surface every runbook uses.
- [Dashboard](/docs/mdndr/operating-guide/dashboard) — the entry point for most triage runbooks via the Recent Alerts widget.
- [Detection Overview](/docs/mdndr/operating-guide/detection-overview)— background on the six detection families that produce runbook triggers.
- [Severity and Confidence](/docs/mdndr/operating-guide/severity-and-confidence) — the severity label definitions that runbook decision trees rely on.
