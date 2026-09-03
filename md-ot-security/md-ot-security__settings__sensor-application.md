<!-- source: https://www.opswat.com/docs/md-ot-security/settings/sensor-application -->

# Sensor - Application

The interval setting is accessible under **Settings > Application.**

## [Operations](/docs/md-ot-security/settings/sensor-application#operations)

### [IP ranges for Internal Network](/docs/md-ot-security/settings/sensor-application#ip-ranges-for-internal-network)

We capture all network traffic. In some cases, customers use non-private IPs (highlighted in the picture below), and previously, we did not create devices for them by default. Now, we also support creating devices with non-private IPs.

This configuration allows the system to identify which IP addresses should be considered part of the **internal network**. These ranges are typically used for:

- Create a device on Asset List

**Private IP ranges and address default**: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16

**Customized (additional) IP ranges:**

- **Purpose**: Support for adding customized non-private IP ranges to the internal hosts.
- **Format**: Must be entered in **CIDR notation** (e.g., 172.168.0.0/16).
- **Validation**: The input field typically requires a valid CIDR address; incorrect formats will be rejected.
- **Actions**:

  - **Add (+)**: Click the plus icon to add more fields for additional ranges.
  - **Remove (–)**: Remove a range by clicking the minus icon next to it.
  - **Save Configuration:** Once the ranges are entered, click **Save** to apply.

### [Network traffic capture frequency options for passive monitoring/discovery](/docs/md-ot-security/settings/sensor-application#network-traffic-capture-frequency-options-for-passive-monitoringdiscovery)

**Purpose:**

This setting controls **how often the system samples and captures network traffic** for analysis.

- **Higher frequency** → More real-time and detailed visibility of applications, devices, and communications.
- **Lower frequency** → Less system load, but less granularity in monitoring.

**Available Options:**

- **1x** → Normal rate (baseline capture frequency). Lowest resource usage.
- **2x (default)** → Twice the normal sampling rate. More responsive detection at a moderate CPU/memory cost.
- **4x** → Highest frequency. Best for near real-time monitoring, but uses the most resources.

### [Chart](/docs/md-ot-security/settings/sensor-application#chart)

Configure chart display.

Number of protocols displayed on charts (prioritize ICS protocols)

## [Asset Learning Duration](/docs/md-ot-security/settings/sensor-application#asset-learning-duration)

Every device in the network scanned into MetaDefender OT Security will be assigned a default compulsory learning hour. After finished the learning hours, if Anomaly detection mode is not turned on, MetaDefender OT Security will or will not keep learning the device behavior afterward.

## [System Setting](/docs/md-ot-security/settings/sensor-application#system-setting)

### [Sound volume](/docs/md-ot-security/settings/sensor-application#sound-volume)

Adjust the volume of on-screen alerts.

### [Operation time info](/docs/md-ot-security/settings/sensor-application#operation-time-info)

Information on the time operation of MetaDefender OT Security: Timezone, First run, Last restarted
