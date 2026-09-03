<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/dashboard -->

# Dashboard

The MetaDefender NDR Dashboard is the default landing surface for authenticated operators. It collects near real-time detection, traffic, and health telemetry in a widget grid. Analysts use the grid to see the environment state before they start an investigation. This chapter explains the default layout. It also explains refresh behavior, widget customization, widget sources, and widget interpretation.

This guide is for Tier 1, 2, and 3 Security Operations Center (SOC) analysts, threat hunters, and system administrators. It assumes a deployment with user access. It also assumes at least one active sensor that feeds events.

First-use acronym expansions in this chapter:

- SOC — Security Operations Center.
- KPI — Key Performance Indicator.
- MITRE ATT&CK — Adversarial Tactics, Techniques, and Common Knowledge.
- ML — machine learning.
- IP — Internet Protocol.
- TCP / UDP / ICMP / SCTP / GRE / VLAN — network protocol abbreviations.
- CPU — central processing unit.
- PDF / PNG / CSV — export formats.

## [Overview](/docs/mdndr/operating-guide/dashboard#overview)

The Dashboard answers the question *"what is the state of the environment right now?"* Operators use it to:

- Confirm the detection pipeline is producing alerts and the sensor plane is capturing traffic.
- Spot spikes in alert volume, severity, or a specific signature before analysts report them as incidents.
- Review the top entities (source IPs, destination IPs, destination ports, signatures) contributing to recent detections.
- Verify host-side health of the Manager and sensor fleet (CPU, memory, capture statistics).
- Launch a focused investigation by opening a recent alert in the shared Hunt sidebar.

The Dashboard is a **snapshot surface**, not a pivot surface. With one exception, widgets do not deep-link into the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). The exception is Recent Alerts. Operators who must pivot on an entity value do it manually from Hunt. This is an intentional separation of concerns: the Dashboard exists to orient the analyst, and the Hunt page exists to investigate.

*Subject:* Analyst home dashboard. The default Analytics tab is open. It shows Top Source IPs, Top Destination IPs, Top Destination Ports, Top Signature Hits, Recent Severities, and Recent Alerts.

## [The default Dashboard](/docs/mdndr/operating-guide/dashboard#the-default-dashboard)

The Dashboard ships with two built-in tabs. Operators land on Analytics on first login; both tabs are closeable and can be re-opened from the tab bar.

| Tab | Purpose | Widgets |
| --- | --- | --- |
| **Analytics** | Detection-facing overview -- who or what is triggering alerts | Top Source IPs, Top Destination IPs, Top Destination Ports, Top Signature Hits, Recent Severities, Recent Alerts |
| **System** | Platform-facing overview -- is the pipeline healthy | Network Capture Statistics, Rules Engine Counters, CPU Performance, Network Decoder Counts, Global Memory Utilization |

### [Tab model](/docs/mdndr/operating-guide/dashboard#tab-model)

The product-wide tab framework manages tabs. Operators can close a tab with the close control on the tab header. Operators can re-create Analytics or System tabs from the `+` menu in the tab bar. Tab state persists per user. If an operator closes Analytics and opens System, the next login restores that configuration.

### [Analytics tab layout](/docs/mdndr/operating-guide/dashboard#analytics-tab-layout)

The Analytics tab uses a three-row grid:

1. **Row 1** -- three equal columns: *Top Source IPs* - *Top Destination IPs* - *Top Destination Ports*.
2. **Row 2** -- two columns in a 2:1 ratio: *Top Signature Hits* (wider) - *Recent Severities* (narrower).
3. **Row 3** -- one full-width row: *Recent Alerts* (paginated table).

### [System tab layout](/docs/mdndr/operating-guide/dashboard#system-tab-layout)

The System tab uses a two-row grid:

1. **Row 1** -- three equal columns: *Network Capture Statistics* - *Rules Engine Counters* - *CPU Performance*.
2. **Row 2** -- two equal columns: *Network Decoder Counts* - *Global Memory Utilization*.

## [Real-time stream and pause / resume](/docs/mdndr/operating-guide/dashboard#real-time-stream-and-pause--resume)

The Dashboard targets near real-time visibility with sub-10-second end-to-end latency and refreshes by periodic poll on MVP. Two page-level controls govern refresh behavior, and two manual controls force an immediate refetch.

| Control | Location | Effect |
| --- | --- | --- |
| **Historic interval** | Sticky header, left selector | Sets the back-window every widget queries against. Options: *Last 1hr*, *Last 2hrs*, *Last 3hrs*, *Last 6hrs*, *Last 12hrs*, *Last 24hrs*, *Last 7 days*, *Last 30 days*. Default: *Last 1hr*. |
| **Reloading interval** | Sticky header, right selector | Sets the auto-refresh cadence for every widget on the page. Options: *Every 10 seconds*, *Every 30 seconds*, *Every 1 minute*, *Every 5 minutes*, *Every 10 minutes*, *Every 30 minutes*, *Every 1 hour*. Default: *Every 5 minutes*. |
| **Manual page refresh** | Sticky header, refresh icon | Forces every widget on the current tab to refetch immediately. |
| **Manual widget refresh** | Per-widget header, refresh icon | Forces a single widget to refetch immediately, independent of the page tick. |
|  |  |  |

### [Pause / Resume](/docs/mdndr/operating-guide/dashboard#pause--resume)

Operators can study a stable snapshot. Select the longest reloading interval to pause auto-refresh. Select a shorter cadence to resume updates. A later release will add a dedicated global *Pause / Resume* toggle for streaming ingestion. See *Roadmap* below.

### [Latency characteristics](/docs/mdndr/operating-guide/dashboard#latency-characteristics)

Widget refresh is driven by periodic poll against the Analytics Application Programming Interface (API), Prometheus, and Elasticsearch. Under the default *Every 5 minutes* cadence, the most recent alert appears on the Dashboard within five minutes of landing in storage. If operators need tighter feedback, they set the cadence to *Every 10 seconds* or *Every 30 seconds*. This increases query load on the backing services. Very large historic windows, such as *Last 7 days* and *Last 30 days*, increase query latency and sample counts. Operators widen the historic window only when they need the longer view.

## [Customize layouts](/docs/mdndr/operating-guide/dashboard#customize-layouts)

Each user can configure the Dashboard grid. Operators use the gear icon in the sticky header to enter configuration mode. In configuration mode, each widget slot shows controls. The controls let operators swap the widget, adjust the slot ratio, or remove the slot.

A later release will add drag-and-drop widget position control. It will also add named user-defined dashboards and the full save / rename / duplicate / delete lifecycle. The *Roadmap* section lists these items. On MVP, layout customization applies to the two built-in tabs.

| Action | How | Persistence |
| --- | --- | --- |
| **Swap a widget** | In configuration mode, open the widget selector in a slot header and choose a different widget. | Saved per user. |
| **Resize a slot** | In configuration mode, adjust the slot's ratio control. | Saved per user. |
| **Remove a slot** | In configuration mode, click the delete control on the slot. | Saved per user. |
| **Add a tab** | Click the `+` on the tab bar and select *Analytics* or *System*. | Saved per user; tabs persist across sessions. |
| **Close a tab** | Click the close control on the tab header. | Saved per user. |
| **Reset a tab** | Close the tab, then re-open it from the `+` menu to return to the default layout. | Saved per user. |

## [Widget catalog](/docs/mdndr/operating-guide/dashboard#widget-catalog)

The table below lists every widget referenced by the Dashboard. Widgets marked **MVP** ship in the default tabs. The Dashboard Functional Requirements Document (FRD) specifies widgets marked **Roadmap**. Those widgets will ship in a later release.

| Widget | Family | Visualization | Data Source | Drill-Down | Status |
| --- | --- | --- | --- | --- | --- |
| **Top Source IPs** | Top-N | Horizontal bar chart, 10 bars ordered by alert count | Analytics API (`AlertBySrcIpHourly`) | None (manual pivot on Hunt) | MVP |
| **Top Destination IPs** | Top-N | Horizontal bar chart, 10 bars | Analytics API (`AlertByDestIpHourly`) | None (manual pivot on Hunt) | MVP |
| **Top Destination Ports** | Top-N | Horizontal bar chart, 10 bars | Analytics API (`TopAlertsByPortAnalytic`) | None (manual pivot on Hunt) | MVP |
| **Top Signature Hits** | Top-N | Horizontal bar chart, 10 bars; long signature names wrap at 24 characters | Analytics API (`TopAlertsBySignature`) | None (manual pivot on Hunt) | MVP |
| **Recent Severities** | Detection | Doughnut chart with segments for Critical, High, Medium, Low, Unknown | Analytics API (`AlertBySeverityHourly`) | None | MVP |
| **Recent Alerts** | Detection | Ontology-driven table, 10 rows per page | Elasticsearch Universal API (`AlertBase` index) | **Yes** -- row action opens the Hunt sidebar in place | MVP |
| **Network Capture Statistics** | Network activity | Bar chart -- three bars: Captured, Dropped, Error | Prometheus counters (`suricata_capture_*`, `suricata_decoder_*`) | None | MVP |
| **Network Decoder Counts** | Network activity | Bar chart -- ten bars: IPv4, IPv6, Ethernet, TCP, UDP, ICMPv4, ICMPv6, SCTP, GRE, VLAN | Prometheus counters (`suricata_decoder_*_packets_total`) | None | MVP |
| **Rules Engine Counters** | Network activity | Bar chart -- two bars: Alerts, Rules | Prometheus counters (`suricata_detect_*`) | None | MVP |
| **CPU Performance** | System health | Line chart, three series: User, System, Idle | Prometheus range query (`node_cpu_seconds_total` by mode) | None | MVP |
| **Global Memory Utilization** | System health | Line chart, three series: Used, Available, Total | Prometheus range queries (`node_memory_*_bytes`) | None | MVP |
| **Threat Overview KPIs** | Summary KPI card | KPI cards with trend arrows for total alerts, critical alerts, unique threat actors, anomaly count, risk score | Analytics API | Planned | Roadmap |
| **Event Volume Over Time** | Time series | Interactive line / area chart of event volume by type and severity | Analytics API | Planned | Roadmap |
| **Top Protocols** | Top-N | Pie or donut chart of protocol distribution | Analytics API | Planned | Roadmap |
| **Top Threat Actors / MITRE Techniques** | Summary KPI card | Treemap or heatmap | Analytics API | Planned | Roadmap |
| **File Extraction Summary** | File scanning | Table of recently extracted files with MetaDefender Core risk scores | Elasticsearch Universal API over `FileInfoEvent` | Planned | Roadmap |
| **Anomaly Score Trend** | ML | Line chart of ML anomaly scores over time with configurable thresholds | ML detections API | Planned | Roadmap |

### [Notes on widget behavior](/docs/mdndr/operating-guide/dashboard#notes-on-widget-behavior)

- **Top-N bar labels** smooth visually for presentation. The displayed bar length on Top-N widgets includes a small cosmetic offset. Thus, the chart remains readable when counts are close. The server-side totals are authoritative. Operators who need exact counts use the [Hunt page](/docs/mdndr/operating-guide/hunt-page) quick-filter and column aggregate.
- **Recent Alerts sidebar.** Opening an alert row mounts the same Hunt sidebar used on the Hunt Page. The sidebar renders the full event detail with entity enrichments, flow context, and file-scan results where available. Closing the sidebar returns to the Dashboard; sidebar state does not survive a page refresh.
- **Top-N pivots.** The four Top-N widgets do not click through. Operators can investigate a source IP, destination IP, destination port, or signature. Copy the value from the widget label. Apply the value as a filter on the Hunt page.
- **Rules Engine Counters label.** The widget header reads *"Rules Engine Encounters"* in the current build; the value is the count of rule encounters (alerts plus loaded rules).
- **Top Destination Ports field contract.** The server response for Top Destination Ports currently exposes a loosely-typed field contract. A subsequent release will add the ontology-backed type. Operators see correct values but may observe empty entries if the backing query returns an unexpected shape.

## [Visualization types](/docs/mdndr/operating-guide/dashboard#visualization-types)

The Dashboard widget framework supports the following visualizations as it matures. The MVP column lists which visualization types shipped widgets use. The remainder are Roadmap. The Dashboard FRD specifies them.

Every widget will support filters, drill-down to a pre-filtered [Hunt Page](/docs/mdndr/operating-guide/hunt-page), and export of underlying data after the platform exposes those capabilities.

| Visualization | Status | Used By |
| --- | --- | --- |
| **Bar chart** (vertical, horizontal, stacked, grouped) | MVP**Bar chart** (vertical, horizontal, stacked, grouped) | Top Source IPs, Top Destination IPs, Top Destination Ports, Top Signature Hits, Network Capture Statistics, Network Decoder Counts, Rules Engine Counters |
| **Pie / donut chart** | MVP**Pie / donut chart** | Recent Severities (donut) |
| **Line / area chart** (time series, zoom) | CPU Performance, Global Memory Utilization | MV**Line / area chart** (time series, zoom) |
| **Heatmap / treemap** | -- | Roadmap**Heatmap / treemap** |
| **Sankey diagram** (network flow visualization) | -- | Roadmap**Sankey diagram** (network flow visualization) |
| **Geographic map** (GeoIP-based) | -- | Roadmap**Geographic map** (GeoIP-based) |
| **MITRE ATT&CK heatmap / matrix** | -- | Roadmap**MITRE ATT&CK heatmap / matrix** |
| **KPI card** (number, trend arrow, sparkline) | -- | Roadmap**KPI card** (number, trend arrow, sparkline) |
| **Top-N list / table** | Recent Alerts (ontology-driven table) | MVP**Top-N list / table** |
| **Attack storyline / timeline** | -- | Roadmap**Attack storyline / timeline** |

## [MITRE ATT&CK framework dashboard](/docs/mdndr/operating-guide/dashboard#mitre-attck-framework-dashboard)

A dedicated, out-of-the-box MITRE ATT&CK Framework Dashboard is part of the MetaDefender NDR roadmap. When delivered, it will:

- Present the enterprise MITRE ATT&CK matrix as an interactive heatmap colored by the count of detections per technique.
- Surface only the subset of tactics and techniques the MetaDefender NDR detection pipeline observes (not the full external matrix), so the heatmap reflects achievable coverage.
- Support drill-down from a technique cell into a Hunt page tab. The tab is pre-filtered to alerts mapped to that technique. The Dashboard propagates the historic interval.
- Refresh on the page tick with no additional configuration, using the same backing real-time pipeline as the Analytics tab.

MITRE technique mappings are already attached to alerts by the detection pipeline, and operators filter on technique identifiers today on the [Hunt Page](/docs/mdndr/operating-guide/hunt-page).

## [Filter across the Dashboard](/docs/mdndr/operating-guide/dashboard#filter-across-the-dashboard)

On MVP, every Dashboard widget honors a single shared filter: the **historic interval** selected in the sticky header. When an operator changes the historic interval, each widget queries the new back-window. The effect appears on the next page tick or immediately after a manual page refresh.

Additional cross-cutting filters -- event type, severity, MITRE technique, threat actor, source or destination entity, protocol -- are Roadmap. The Dashboard FRD specifies these as page-level filters. For example, if an operator selects *severity = Critical* in a future release, each widget uses the same severity constraint. On MVP, operators who need to narrow by any of these dimensions do so on the Hunt page, which applies the full filter grammar.

## [Exporting](/docs/mdndr/operating-guide/dashboard#exporting)

Export of dashboard views and data is **Roadmap**. The Dashboard FRD defines exports to Portable Document Format (PDF), Portable Network Graphics (PNG), and Comma-Separated Values (CSV). The planned behavior is:

- **PDF** -- full-page render of the current tab, preserving widget order and the active historic interval.
- **PNG** -- per-widget and full-tab image export.
- **CSV** -- export of the backing dataset for any data-bearing widget (Top-N, Recent Alerts, Severities, Prometheus counters).

Operators can extract underlying data from the Hunt page with row selection and download. Operators can also use the integrations layer: Security Information and Event Management (SIEM) forwarding or Syslog.

## [Drill-down behavior](/docs/mdndr/operating-guide/dashboard#drill-down-behavior)

One widget supports in-place drill-down on MVP.

| Widget | Drill-Down Path | What Opens |
| --- | --- | --- |
| **Recent Alerts** | Row action button on any alert row | The Hunt page sidebar mounted in place, showing the full alert with entity enrichments, flow context, and file-scan results |

All other widgets are **non-interactive** on MVP -- chart bars, doughnut segments, and time-series points do not click through. Operators can investigate an entity value from a Top-N or KPI widget. Copy the value. Apply it as a Hunt page filter with the quick-filter or the right-click pivot on the detail sidebar. The Hunt page chapter documents both pivot paths.

The Dashboard FRD target for the full MVP end-state is click-to-filter drill-down from every widget to a pre-filtered Hunt page tab. *Roadmap* tracks this target.

## [See also](/docs/mdndr/operating-guide/dashboard#see-also)

- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) -- the primary investigation surface, reached manually from Dashboard entity values and automatically from the Recent Alerts row action.
- [Daily Operations](/docs/mdndr/operating-guide/daily-operations) -- the daily cadence that uses the Dashboard as its first checkpoint.
- [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring) -- deeper view of platform health than the System tab exposes.
