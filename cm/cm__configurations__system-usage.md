<!-- source: https://www.opswat.com/docs/cm/configurations/system-usage -->

# System Usage

The **System Usage** feature helps administrators monitor the My OPSWAT Central Management server's health status, which include the health status of its system service and the host machine's resource usage metrics: memory, CPU and disk usage.

Administrators can configure usage thresholds and enable automated email alerts for any system health and usage issues.

> **Version requirement**
>
> System Usage is available in My OPSWAT Central Management **10.7.26092 and later**. On earlier versions the feature is not visible and the **System Usage** tab does not appear under **Settings → Servers**.

**In This Guide**

- [System Usage Dashboard](https://www.opswat.com/docs/cm/configurations/system-usage#system-usage-dashboard)
- [Email Notification Configuration](https://www.opswat.com/docs/cm/configurations/system-usage#email-notification-configuration)

## System Usage Dashboard

Navigate to **Settings > Servers > **Open** System Usage **tab to begin.

![](https://uploads.developerhub.io/prod/97qW/37bnhvk3ue4xove0jwb4et2ivrtyrr7bjhdb17ikg0umwifudmb7k6tq3udsfxvf.png)

The **System Usage **tab provides a dashboard view of the host machine's resource usage. The following metrics are available:

- CPU
- Memory
- Disks that are used by the My OPSWAT Central Management installation.

## Email Notification Configuration

The setting sections below the dashboard let admins configure email notification feature. Please note that [Email Server](https://www.opswat.com/docs/cm/configurations/email-server) must be configured to use this feature.

The **General **section configures how the email notifications are evaluated and sent.

![](https://uploads.developerhub.io/prod/97qW/et7fox617jvh54z6ou34zlkcp99v3l3ul8zoi07xga03scsad4gguapw8h8hni6s.png)

- **Check Frequency:** The frequency of individual health checks.
- **Notify When Condition Persists For: **The amount of consecutive failed checks required for sending email notifications.
  - For example, if a subcomponent or a resource metric (such as memory usage) is in a failure state for 3 consecutive checks (which ~6 minutes at 2-minute frequency) then an email notification will be triggered

> On server startup, the threshold for **Notify When Condition Persists For** is configured to be twice of the current setting to allow for startup time.
>
> That is, if the setting is set to 3 consecutive checks then on startup, an email notification will only be sent after 6 consecutive failed checks.

The **System Service, Disk Space, CPU **and **Memory** sections configure the individual email notification settings for each type of server health issues.

![](https://uploads.developerhub.io/prod/97qW/rdxwu3ksrib0hokvavp1nrlpnjowya3yuyc1ioj3nbde4tv8nzvd7j2rkwdf7qdw.png)

![](https://uploads.developerhub.io/prod/97qW/gqb4uk5sf24o2hfjjqxqoe27gf4efzug193myijx71gxcn4d827jp0lus48sql0v.png)

![](https://uploads.developerhub.io/prod/97qW/tebfd61hyuh1ndk5tbofgyjwqfcq1t4f1jmi1pvj776mpv84c35e4towp7nub62x.png)

![](https://uploads.developerhub.io/prod/97qW/r51t8qj6tfeh4p6pyaw6n2r7iuh0a58c4vyg31mi3776w9zvtflpadzk6zgpjmfx.png)

- **Enabled:** Enable email notification for each issue type.
- **Threshold: **The alert threshold for each resource metric type, by percentage.
- **Severity:** The severity level of each issue type, for information purpose. This information will be included in the email notifications.
- **Recipients:** The recipient email addresses.
- **Email Subject:** The customizable email subject.

> To account for oscillation, which can cause email spamming, each type of health issues requires 3 consecutive success checks for transition from failure to success state.
>
> For example, with a memory usage threshold of 90%, the memory usage must remain below 90% for 3 consecutive checks before the memory health status can be changed from failure to success state.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
