<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/endpoint-performance-monitoring -->

# Endpoint Performance Monitoring

**Endpoint Performance Monitoring** gives administrators real-time visibility into the health and workload of managed Windows endpoints. It provides:

1. **Performance monitoring:** Live charts displaying real-time CPU, Memory, Disk activity, and Network traffic while the administrator has the device page open. See [How to View Endpoint Performance.](https://www.opswat.com/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#how-to-view-endpoint-performance)
2. **Incidents history:** Automatically generate incident logs and alerts when usage stays above safe limits for too long. See [How to Set Up Alert Thresholds.](https://www.opswat.com/docs/cm/endpoint-security-solution/endpoint-performance-monitoring#how-to-set-up-alert-thresholds)

![](https://uploads.developerhub.io/prod/97qW/aza92yrknvbfporfd5uv6i372jxuyy41v02v6mn9g7m6znn2dqolte19beteq4zs.png)

## **Supported Platforms & Requirements**

| Requirement | Details |
| ---- | ---- |
| **Supported OS** | **Windows** *(macOS and Linux are currently not supported)* |
| **Console Version** | Cloud or On-Premises (Release **10.7.26092** or later) |
| **Persistent Agent** | Version** 7.6.2609.1108 or later** |
| **On-Demand Agent** | Version** 7.3.2609.530 or later** |

## How to View Endpoint Performance

1. In the left navigation bar, go to **Inventory** > **Devices**
2. Select a Endpoint **Windows **device
3. Click the **Performance** tab from the top menu bar.

**Endpoint Performance**

![](https://uploads.developerhub.io/prod/97qW/boh821abkjkl95anyj7vnihna8awp2k3jg7z6qlkjzsyg4gcb6nqbkdjalyf4fsa.png)

- Shows live usage data for CPU, Memory, Disk Read/Write, and Network
- Data updates automatically every 30 seconds
- When you open the tab, the agent begins streaming telemetry. Polling automatically stops a few minutes after you leave the tab to save bandwidth

**Incidents History**

![](https://uploads.developerhub.io/prod/97qW/rbnjv7ifmgbvj0dwyr5rl7i0g75kbjvrmp1ixxalyzvcux1lquurvkg2tuq6orzs.png)

- Displays total incident trends grouped across your selected timeframe (1 hour, 24 hours, or 7 days).
- Lists every sustained threshold breach recorded over the past 7 days
- Incident records are automatically stored for 7 days.

## **How to Set Up Alert Thresholds**

An incident is created only when a metric exceeds its threshold **continuously for the full duration specified**. This prevents false alarms from short, temporary spikes.

### **Set Global Rules (Applies to all devices)**

![](https://uploads.developerhub.io/prod/97qW/tzudnyws9p9ji3l0oyzg1tiulh4ewu46a4y7ag7qcumuwvk9zpdqklmw7rfqgags.png)

1. Go to **Settings** > **Global** > **Endpoint Clients**
2. Scroll down to the **Performance Alerts** section
3. Select any rule you want to activate
4. Enter your desired **Threshold** and **Duration (in minutes)**
5. Click **Save**

### **Set Group-Specific Rules**

![](https://uploads.developerhub.io/prod/97qW/e3h4tn15o4j1vnemwpglkxijuigzdmfdfgxtsw3wxuhptgbz3rvzd0135lc2u69z.png)

1. Go to **Inventory** > **Groups** and select your target endpoint group
2. Open **Settings **tab
3. Under **Performance Alerts**, configure the threshold and duration values for this group
4. Click **Save**

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
