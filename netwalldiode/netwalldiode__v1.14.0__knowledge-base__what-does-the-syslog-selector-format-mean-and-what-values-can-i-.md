<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i- -->

# What does the syslog selector format mean and what values can I set in MetaDefender Optical Diode?

This article applies to all MetaDefender Optical Diode Versions

## [Overview](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#overview)

This knowledge base article explains the syslog selector format, including facilities and severity levels, and how they apply when configuring syslog forwarding for OPSWAT MetaDefender Diode deployments. Proper configuration ensures that relevant security and operational events are captured, filtered, and forwarded to external systems such as SIEM platforms.

---

## [**What is a Syslog Selector?**](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#what-is-a-syslog-selector)

A **syslog selector** defines which log messages should be captured and processed based on two attributes:

`<facility>.<severity>`

- **Facility** → Identifies the source or category of the log message
- **Severity** → Indicates the importance or urgency of the message

---

### [**Relevance to MetaDefender Diode**](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#relevance-to-metadefender-diode)

- OPSWAT MetaDefender Diode typically uses **local facilities (e.g.,** `local6`**)**
- This allows separation of OPSWAT logs from OS/system logs
- Recommended best practice is to dedicate a single local facility (e.g., `local6`) exclusively for MetaDefender Optical Diode logs.

---

## [**Syslog Facility Values**](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#syslog-facility-values)

Facilities categorize where logs originate. Syslog defines standard facilities as well as custom ones.

### [**Common Standard Facilities**](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#common-standard-facilities)

| Facility | Description |
| --- | --- |
| auth / authpriv | Authentication-related messages |
| daemon | System services and background processes |
| kern | Kernel messages |
| syslog | Syslog internal messages |
| user | User-level processes |
| mail | Mail system |
| cron | Scheduled jobs |
| lpr | Printing subsystem |

### [**Custom (Local) Facilities**](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#custom-local-facilities)

| Facility | Description |
| --- | --- |
| local0 – local7 | Reserved for custom applications and devices |

---

## [**Syslog Severity Levels**](/docs/netwalldiode/v1.14.0/knowledge-base/what-does-the-syslog-selector-format-mean-and-what-values-can-i-#syslog-severity-levels)

Severity defines how critical a message is. Lower numbers indicate higher urgency.

If you have any questions on how this setup works and/or are having issue getting replication to work successfully, please reach out to our OPSWAT Support Team.

| Level | Keyword | Description |
| --- | --- | --- |
| 0 | emerg | System is unusable |
| 1 | alert | Immediate action required |
| 2 | crit | Critical condition |
| 3 | err | Error condition |
| 4 | warning | Warning condition |
| 5 | notice | Normal but significant |
| 6 | info | Informational messages |
| 7 | debug | Debug-level messages |

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).

MetaDefender
