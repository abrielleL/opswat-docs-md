<!-- source: https://www.opswat.com/docs/md-ot-security/operating/enterprise-dashboard -->

# Enterprise dashboard

## [Enterprise dashboard](/docs/md-ot-security/operating/enterprise-dashboard#enterprise-dashboard)

The **Dashboard** is the main overview you see after you sign in to the MetaDefender OT Security web console when you are working at **enterprise** level (your browser tab usually shows **Enterprise** in the title). The screen summarizes activity for whatever you currently have selected—often the whole deployment, a specific site, or a sensor. Use the **scope** control in the header (it shows the current selection, such as a sensor name) to switch context; charts and numbers update to match that selection.

## [Opening the dashboard](/docs/md-ot-security/operating/enterprise-dashboard#opening-the-dashboard)

| Step | What to do |
| --- | --- |
| 1 | Open a web browser and go to the **MetaDefender OT Security address** your administrator gave you (it is normally an `https://` link to your organization’s server). |
| 2 | Sign in with the account you were provided. |
| 3 | Make sure you are in **Monitor** mode—the everyday monitoring experience. If you see **Management**-style options instead, click **Go to Monitor** in the sidebar to return to monitoring. |
| 4 | In the left sidebar, click **Dashboard**. It is usually the first item at the top of the menu. |
| 5 | *(Optional)* To change what you are looking at, open the **menu in the header** that shows the current region, site, or sensor, then pick **Enterprise**, a **site**, or a **sensor** so the dashboard matches what you need to review. |

## [Header strip](/docs/md-ot-security/operating/enterprise-dashboard#header-strip)

| Area | What it is for |
| --- | --- |
| **CPU / RAM / Disk** | How busy the console host is (processor, memory, and disk). |
| **Tx / Rx** | Approximate send and receive traffic for the scope you selected. |
| **Scope / region selector** | Lets you switch between enterprise-wide view, sites, or sensors, depending on how your environment is set up. |
| **Language** | Changes the interface language where supported. |
| **Notifications and account** | Alerts, profile, and similar controls. The **Alerts** item in the sidebar may show a count badge when there are open alerts. |

## [Main widgets (typical layout)](/docs/md-ot-security/operating/enterprise-dashboard#main-widgets-typical-layout)

What you see can vary slightly by product version and your role. Typical widgets include:

| Widget | What it shows |
| --- | --- |
| **Protocols (Today)** | Industrial and IT protocols observed today, often as a chart over time. |
| **Connection Alert Matrix (Today)** | How **connection** alerts line up by severity and asset level for today. |
| **Asset Alert Matrix (Today)** | How **asset** alerts line up by severity and level for today. |
| **Total Internal Connections** | A high-level count of internal connections from recorded history. |
| **Total Connections with External** | A high-level count of connections involving external systems. |
| **Asset Types** | How many assets fall into each category (for example PLCs, HMIs, workstations), often with a **Total assets** figure. |

*(Image could not be embedded — see Confluence)*

## [Related areas](/docs/md-ot-security/operating/enterprise-dashboard#related-areas)

| Area | Purpose |
| --- | --- |
| **Assets** | Browse and open details for discovered assets. |
| **Network Map** | See a map-style view of the network. |
| **Connections** | Dig into connections between endpoints. |
| **Alerts** | Review and work through alerts. |
| **Settings** | Change configuration; this may switch you into **Management** for deeper enterprise settings. |

## [Notes](/docs/md-ot-security/operating/enterprise-dashboard#notes)

- The numbers and charts on your screen depend on **your live environment**, traffic, and how long data is kept—not on fixed demo values.

- Tasks such as licensing, backups, or other **enterprise-only** configuration are covered under **Settings** and the **Enterprise Settings** documentation, not only on this dashboard page.
