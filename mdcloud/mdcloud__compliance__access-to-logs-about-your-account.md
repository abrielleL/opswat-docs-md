<!-- source: https://www.opswat.com/docs/mdcloud/compliance/access-to-logs-about-your-account -->

# Access to logs about your account

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

### [Records you can get yourself](/docs/mdcloud/compliance/access-to-logs-about-your-account#records-you-can-get-yourself)

| Record | Where to find it |
| --- | --- |
| **Scan history and scan results** | In [metadefender.com](http://metadefender.com), under your scan history. A single scan result can be exported as a PDF. |
| **Scan history through the API** | `GET /v4/apikey/scan-history` returns the scan history of your API key in JSON format. To convert it to CSV, see [How do I export MetaDefender Cloud scan history as CSV?](https://www.opswat.com/docs/mdcloud/knowledge-base/how-do-i-export-metadefender-cloud-scan-history-as-csv-) |
| **API usage** | Dashboard → [Usage](https://www.opswat.com/docs/mdcloud/operation/usage). Shows the calls made per day and per hour, split by Prevention, Reputation and Sandbox, for up to the last 365 days or a custom date range. Organisation administrators can also view each sub-organisation. |
| **Account events** | Settings → [Notifications](https://www.opswat.com/docs/mdcloud/account-management/notifications-and-alerts). Administrators can be notified when a user is added or removed, when a role changes, when a request is refused because its IP address is outside the allowlist, and when usage reaches a threshold they set. |
| **Events in your own SIEM** | MetaDefender Cloud can forward scan results and account events to your SIEM as they happen. See [SIEM integrations](https://www.opswat.com/docs/mdcloud/integrations/splunk-siem-integration). |

### [What is not shared](/docs/mdcloud/compliance/access-to-logs-about-your-account#-what-is-not-shared)

- **Other customers’ records.** The records we provide contain only the activity of your own account or organisation.
- **Platform infrastructure and security logs.** These cover the whole platform, so they are not shared with any customer. If a security incident affects your data, OPSWAT notifies you as described in [Incident Reporting](https://www.opswat.com/docs/mdcloud/legal/incident-reporting-on-metadefender-cloud).

For how times are recorded and displayed, see [Time and timestamps in MetaDefender Cloud](https://www.opswat.com/docs/mdcloud/operation/time-and-timestamps-in-metadefender-cloud).
