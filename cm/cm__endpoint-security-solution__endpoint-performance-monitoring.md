<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/endpoint-performance-monitoring -->

# Endpoint Performance Monitoring

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**Endpoint Performance Monitoring** gives administrators real-time visibility into the health and workload of managed Windows endpoints. It provides:

1. **Performance monitoring:** Live charts displaying real-time CPU, Memory, Disk activity, and Network traffic while the administrator has the device page open. See [How to View Endpoint Performance.](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#how-to-view-endpoint-performance)
2. **Incidents history:** Automatically generate incident logs and alerts when usage stays above safe limits for too long. See [How to Set Up Alert Thresholds.](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#how-to-set-up-alert-thresholds)

## [**Supported Platforms & Requirements**](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#supported-platforms--requirements)

| Requirement | Details |
| --- | --- |
| **Supported OS** | Windows, macOS, and Linux |
| **Console Version** | Cloud or On-Premises (Release **10.7.26092** or later) |
| **Persistent Agent** | Version **7.6.2609.1108 or later** |
| **On-Demand Agent** | Version **7.3.2609.530 or later** |

## [How to View Endpoint Performance](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#how-to-view-endpoint-performance)

1. In the left navigation bar, go to **Inventory** > **Devices**
2. Select a Endpoint **Windows** device
3. Click the **Performance** tab from the top menu bar.

**Endpoint Performance**

- Shows live usage data for CPU, Memory, Disk Read/Write, and Network
- Data updates automatically every 30 seconds
- When you open the tab, the agent begins streaming telemetry. Polling automatically stops a few minutes after you leave the tab to save bandwidth

**Incidents History**

- Displays total incident trends grouped across your selected timeframe (1 hour, 24 hours, or 7 days).
- Lists every sustained threshold breach recorded over the past 7 days
- Incident records are automatically stored for 7 days.

## [**How to Set Up Alert Thresholds**](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#how-to-set-up-alert-thresholds)

An incident is created only when a metric exceeds its threshold **continuously for the full duration specified**. This prevents false alarms from short, temporary spikes.

### [**Set Global Rules (Applies to all devices)**](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#set-global-rules-applies-to-all-devices)

1. Go to **Settings** > **Global** > **Endpoint Clients**
2. Scroll down to the **Performance Alerts** section
3. Select any rule you want to activate
4. Enter your desired **Threshold** and **Duration (in minutes)**
5. Click **Save**

### [**Set Group-Specific Rules**](/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#set-group-specific-rules)

1. Go to **Inventory** > **Groups** and select your target endpoint group
2. Open **Settings** tab
3. Under **Performance Alerts**, configure the threshold and duration values for this group
4. Click **Save**
