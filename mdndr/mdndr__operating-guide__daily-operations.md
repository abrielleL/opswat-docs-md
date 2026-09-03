<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/daily-operations -->

# Daily Operations

This chapter describes the day-to-day cadence for MetaDefender NDR. It covers the checklist that operators use at the start of each shift. It also covers the daily workflow from ingestion review through tuning. Weekly and monthly activities help keep the deployment healthy. This chapter stays at the routine-operations level. Deep investigation procedures are in [Investigation Runbooks](/docs/mdndr/operating-guide/investigation-runbooks). Administrative procedures are under [Administration Page](/docs/mdndr/operating-guide/administration-page).

This guide is for Tier 1 and Tier 2 Security Operations Center (SOC) analysts, shift leads, and on-call engineers. It assumes a MetaDefender NDR deployment with at least one active sensor. It also assumes a user account with hunting and health-viewing permissions.

First-use acronym expansions in this chapter:

- SOC — Security Operations Center.
- NDR — Network Detection and Response.
- SPAN — Switched Port Analyzer.
- KPI — Key Performance Indicator.
- IOC — Indicator of Compromise.
- IDS / IPS — Intrusion Detection / Prevention System.
- ML — machine learning.
- PCAP — packet capture.
- SLA — service-level agreement.
- TLS — Transport Layer Security.
- RBAC — role-based access control.

## [Daily checklist](/docs/mdndr/operating-guide/daily-operations#daily-checklist)

At the beginning of each shift, operators work through the following checklist. The goal is to confirm platform health. Operators also confirm that the detection pipeline produces events at the expected rate. No high-severity alerts must sit untriaged.

| Area | What to Check | How to check |
| --- | --- | --- |
| **Platform Health** | All sensors and the Manager are online, reporting fresh heartbeats, and ingesting traffic at the expected rate. | Open [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring) and confirm a green status for the Manager and every sensor. Review the sensor heartbeat column, the capture-rate and drop-rate indicators, and the pipeline lag metrics. |
| **Detection Pipeline** | Detections are arriving and the severity distribution is consistent with the prior day. Sudden drops or spikes warrant investigation. | Open the [Dashboard](/docs/mdndr/operating-guide/dashboard). Compare the Recent Severities donut and the Top Signature Hits widget against the previous 24-hour window. Scan Recent Alerts for any activity since the last shift. |
| **High-Severity Alerts** | Operators acknowledged, assigned, or closed each Critical and High alert from the overnight window. Each closed alert has a triage note. | Open the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). Switch to the *All Alerts* tab. Apply a severity filter of Critical or High. Set the time range to cover the gap since the last shift. Work the list from top to bottom. |
| **Updates Currency** | Suricata signatures, InSights feeds, and command-and-control (C2) intelligence are current. No failed update jobs are sitting in an error state. | Open [Administration Page](/docs/mdndr/operating-guide/administration-page) and [updates](/docs/mdndr/operating-guide/updates-management) confirm the last successful update timestamp for each feed. Review any distribution errors surfaced on the sensor targets. |

Operators who find a failing item on the checklist record the observation, apply the relevant runbook, and escalate per the site's incident response procedure. The checklist is intentionally short so it takes under ten minutes when nothing is out of place.

## [Typical daily workflow](/docs/mdndr/operating-guide/daily-operations#typical-daily-workflow)

The routine daily workflow follows the checklist with investigation, tuning, and handoff activities woven in. Each step is self-contained; analysts may skip steps that the checklist has already cleared.

1. **Review platform health and ingestion.** Confirm sensor heartbeats, capture statistics, and pipeline lag from [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring). If a sensor is offline or drops packets, operators raise the appropriate ticket before alert triage. Gaps in ingestion affect the reliability of the day's work.
2. **Scan the Dashboard for anomalies.** Open the [Dashboard](/docs/mdndr/operating-guide/dashboard). Compare Recent Severities, Top Signature Hits, and Top Source, Destination, and Port widgets with the prior 24-hour baseline. Note any signature or entity that becomes dominant. Note any widget that becomes quiet.
3. **Triage high-severity alerts first.** Apply a Critical + High severity filter on the [Hunt Page](/docs/mdndr/operating-guide/hunt-page) *All Alerts* tab. Work the results oldest-to-newest. For each alert, escalate, downgrade after benign confirmation, or add a triage note. The triage note helps the shift lead see progress.
4. **Investigate priority alerts with the runbook library.** For Critical alerts, analysts switch from triage to investigation. Analysts also investigate High alerts with credible compromise evidence. Common entry points are critical-alert triage, C2 beacon investigation, data-exfiltration investigation, and malicious-file investigation.
5. **Correlate file-related alerts with MetaDefender Core.** If a detection references an extracted file, review the MetaDefender Core enrichment in the alert detail sidebar. If the file does not have a scan result, coordinate with MetaDefender Core operators to submit it. Revisit the alert when the verdict is available. The [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation) covers the full procedure.
6. **Work the medium and low queues.** After analysts clear Critical and High, rotate through Medium and Low severities as time permits. Medium items usually require correlation with other telemetry. Low items are mostly tuning candidates.
7. **Record tuning candidates.** If an alert is consistently benign in the environment, open a tuning ticket against the detection family. Repeated false positives feed the weekly tuning cadence. Operators do not silently suppress alerts from the shift view.
8. **Hand off to the next shift.** The outgoing shift posts a short handover note. The note covers open investigations, alerts that require attention, platform-health anomalies, and tuning tickets. The handover note lets the incoming shift skip completed steps.

## [Weekly cadence](/docs/mdndr/operating-guide/daily-operations#weekly-cadence)

Some activities are cheaper to run once a week than once a day, because they require aggregating observations across multiple shifts.

- **Rule-update review.** Analysts review the previous week's Suricata-signature and InSights-feed updates from [Administration -> Updates](/docs/mdndr/operating-guide/manager-configuration). The review covers release notes for new detection categories, severity changes, and deprecations. Analysts log changes that can shift alert volumes or break existing runbooks.
- **Tuning review.** Shift leads consolidate the week's tuning tickets. These tickets include recurring benign alerts, high-false-positive signatures, and noisy behavioral rules. Shift leads apply the adjustments that the tuning process approves. Policy edits flow through the change-management process rather than ad-hoc edits.
- **Sensor-health review.** Operators review sensor capture-rate and drop-rate trends from [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring) for the previous seven days. Sustained drops or sustained increases in pipeline lag raise a capacity or configuration question that the administrator addresses before it becomes a coverage gap.
- **Backlog review.** Shift leads review open investigations that continued for more than one shift. They close them, escalate them, or assign an explicit owner.

## [Monthly cadence](/docs/mdndr/operating-guide/daily-operations#monthly-cadence)

A small number of activities are appropriate once a month. The goal is to keep deployment design, detection coverage, and data retention aligned with the environment.

- **Sensor-placement review.** Network and security engineering review the current SPAN, tap, and sensor layout against the segments that carry high-value traffic. Any segment that has become important since the last review is either added to the sensor footprint or flagged for the next deployment cycle.
- **Detection-tuning audit.** Administrators review the cumulative effect of a month of tuning changes against the baseline detection library. They remove tuning entries that are no longer necessary. They document tuning entries that materially shifted alert volumes in the site's detection runbooks.
- **Retention review.** Administrators confirm that the [Data Retention](/docs/mdndr/operating-guide/data-retention) settings still match the environment's storage footprint and any compliance obligations. Administrators adjust retention windows through the administration interface. Retention windows include alerts, flows, session records, extracted files, and packet captures. Administrators record changes in the change log.
- **Role and access review.** The shift lead and an administrator review the active user list and role-based access control (RBAC) assignments from [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac). They remove accounts for personnel who no longer require access. They confirm that group-based asset ownership still reflects the current organizational structure.
- **Release-notes check.** For deployments upgraded since the last review, scan the release notes for features that moved from preview to general availability. Adjust local runbooks where labels or behavior changed.

## [See also](/docs/mdndr/operating-guide/daily-operations#see-also)

- [Dashboard](/docs/mdndr/operating-guide/dashboard) -- the first checkpoint on the daily checklist.
- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) -- the primary triage and investigation surface referenced throughout the daily workflow.
- [Investigation Runbooks](/docs/mdndr/operating-guide/investigation-runbooks) -- deep procedures for the investigation step of the daily workflow.
- [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring) -- backing detail for the platform-health checks at the start of each shift and the sensor-health review each week.
- [Updates Management](/docs/mdndr/operating-guide/updates-management) -- the surface operators use to confirm update currency daily and to plan rule reviews weekly.
