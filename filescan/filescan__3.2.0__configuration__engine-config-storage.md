<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/engine-config-storage -->

# Storage

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The backend Sandbox engine creates and temporarily stores files like scan results, input files. The retention policy can be adjusted to fit to the throughput and disc size.

To modify the retention policy:

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #2 - Modify the configuration by adding or modifying the following properties:**

transform.cfgCopyrunFileSystemCleanup=true
cleanupCompletedTasksOlderThanXSeconds=600

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Property details](/docs/filescan/3.2.0/configuration/engine-config-storage#property-details)

| Property Name | Default Value | Description |
| --- | --- | --- |
| runFileSystemCleanup | true | Main switch to enable / disable file retention feature |
| cleanupCompletedTasksOlderThanXSeconds | 10 minutes | Retention for specific Sandbox scans Minimum value: 60 |

Info

All other files will be removed daily

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
