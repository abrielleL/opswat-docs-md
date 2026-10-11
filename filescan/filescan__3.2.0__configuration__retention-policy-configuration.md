<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/retention-policy-configuration -->

# Retention Policy Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Configuration on the Admin panel](/docs/filescan/3.2.0/configuration/retention-policy-configuration#configuration-on-the-admin-panel)

You can configure the retention under the Webservice Admin (UX) panel as well.

For that click on the user icon on the top right corner and select "**Admin**" panel:

Then select "**Settings**" in the middle:

Select "**Configuration**":

Under the "**Retention**" tab you can set retention policy:

By default, retention is **enabled** and set to 90 days for malicious samples and 14 days for non-malicious samples.

Note that scan reports are not deleted by default.

### [Configuration options](https://docs.opswat.com/filescan/configuration/ocm#configuration-options)

| Field | Description |
| --- | --- |
| `RETENTION_ENABLED` | Enable or disable data retention |
| `RETENTION_DELETE_REPORT` | Enable or disable deleting retention report |
| `RETENTION_PERIOD_MALICIOUS` | Set retention period for malicious files (the value is in days, set to 0 for indefinite storage) |
| `RETENTION_PERIOD_SUSPICIOUS` | Set retention period for suspicious files (the value is in days, set to 0 for indefinite storage) |
| `RETENTION_PERIOD_INFORMATIONAL` | Set retention period for informational files (the value is in days, set to 0 for indefinite storage) |
| `RETENTION_PERIOD_UNKNOWN` | Set retention period for unknown files (the value is in days, set to 0 for indefinite storage) |
| `RETENTION_PERIOD_BENIGN` | Set retention period for benign files (the value is in days, set to 0 for indefinite storage) |

## [Backend configuration](/docs/filescan/3.2.0/configuration/retention-policy-configuration#backend-configuration)

By default, the system is designed to clean up locally stored results/received samples and other temporary files. These cleanup operations are performed either upon starting up the service (single-pass) or on continuous short-cycle intervals in a background process. To enable regular cleanup during the server mode, make sure the following options are enabled:

| File | Option Name |
| --- | --- |
| broker.cfg | runFileSystemCleanup |
| transform.cfg | runFileSystemCleanup |

---

By default, the following retention period is applied (see “Retention Policy” sections in both broker.cfg and transform.cfg files):

| File | Option Name | Retention Period in minutes |
| --- | --- | --- |
| Analysis Results | deleteResultsPathArtifactsOlderThanXMinutes | 120 (2 hours) |
| Sample Files | deleteStoredSamplesOlderThanXMinutes | 120 (2 hours) |
| Temp Files | deleteTempFilesOlderThanXMinutes | 120 (2 hours) |
| Queued Files | deleteQueueFilesIfOlderThanXMinutes | 120 (2 hours) |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
