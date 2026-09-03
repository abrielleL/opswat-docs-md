<!-- source: https://www.opswat.com/docs/md-ot-security/operating/sensor-dashboard -->

# Sensor Dashboard

## [Sensor dashboard](/docs/md-ot-security/operating/sensor-dashboard#sensor-dashboard)

The **Dashboard** in **Monitor** mode shows a **sensor-oriented** summary when your **scope** is a **site**, **network segment**, or **sensor** (depending on how your deployment is structured). Metrics and charts reflect **recorded history** for the scope you select in the **header menu** (the control that shows the current site, sensor, or similar label). Switch scope there to compare activity across sensors or segments.

## [Opening the sensor dashboard](/docs/md-ot-security/operating/sensor-dashboard#opening-the-sensor-dashboard)

| Step | What to do |
| --- | --- |
| 1 | Open a web browser and go to the **MetaDefender OT Security address** your administrator gave you (normally an `https://` URL). |
| 2 | Sign in with the account you were provided. |
| 3 | Stay in **Monitor** (everyday monitoring). If you see **Management**-style navigation, choose **Go to Monitor** in the sidebar. |
| 4 | In the left sidebar, click **Dashboard**. |
| 5 | Open the **scope** control in the **header** (next to throughput) and pick the **site**, **network segment**, or **sensor** you want this overview to represent. On appliances that combine site and sensor, choose **Built-in sensor** to see the sensor-scoped dashboard below. Labels depend on your environment. |

## [Header strip](/docs/md-ot-security/operating/sensor-dashboard#header-strip)

| Area | What it is for |
| --- | --- |
| **CPU / RAM / Disk** | Resource use on the console host. |
| **Tx / Rx** | Approximate send and receive traffic for the selected scope. |
| **Scope selector** | Switches between enterprise, sites, sensors, or segments so all dashboard tiles stay aligned with that context. |
| **Language** | Changes the interface language where supported. |
| **Notifications and account** | Alerts, profile, and related shortcuts. |

## [Main areas (sensor scope, including Built-in sensor)](/docs/md-ot-security/operating/sensor-dashboard#main-areas-sensor-scope-including-built-in-sensor)

When the header scope is a **sensor** (such as **Built-in sensor**), the dashboard emphasizes that sensor’s traffic and alerts. The exact tiles can vary by version and role; a typical layout includes:

| Section | What it shows |
| --- | --- |
| **Asset types / asset summary** | Counts for major categories (for example **Computer**, **Desktop**, **Industrial device** types) and a **total assets** figure for the current scope. Values come from **recorded history**. |
| **Connection Alert Matrix (Today)** | A grid of **connection** alerts by **asset level** and **alert severity** for today. |
| **Asset Alert Matrix (Today)** | A similar matrix for **asset** alerts for today. |
| **Protocols (Today)** | Small trend views of observed protocols (for example **HTTP**, **S7COMM**, **UDP**, **ARP**, **ICMP**) over the recent window. |
| **Total internal connections** | A distribution of internal connection volume by protocol (often as a chart), with a total from recorded history. |
| **Total connections with external** | Traffic involving external endpoints, broken down by protocol where shown. |

At **enterprise** or **site** scope, you may instead see tiles such as **Asset Status**, **Active Connection Status (Today)**, **Active Connections by Sensor/Network Segment**, and **Alert Status (Today)** with segment breakdowns.

*(Image could not be embedded — see Confluence)*

## [Related areas](/docs/md-ot-security/operating/sensor-dashboard#related-areas)

| Area | Purpose |
| --- | --- |
| **Assets** | Open detailed records for discovered assets. |
| **Network Map** | Topology-style view of the network. |
| **Connections** | Inspect connections between endpoints. |
| **Alerts** | Work through alerts and acknowledgements. |
| **Settings** | Configuration; may switch you into **Management** for deeper options. |

## [Notes](/docs/md-ot-security/operating/sensor-dashboard#notes)

- Numbers and charts depend on **live traffic**, **retention**, and **scope**—they are not fixed demo values.

- If a welcome or status overlay appears when you first open **Monitor**, close it to see the full dashboard tiles.
