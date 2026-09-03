<!-- source: https://www.opswat.com/docs/mdss/operations/scanning -->

# Scanning

This page explains how to configure scans in MetaDefender Storage Security (MDSS) and highlights its unique features.

## [Types of scanning](/docs/mdss/operations/scanning#types-of-scanning)

MetaDefender Storage Security offers three distinct types of scanning to meet your needs: **On-Demand Scan**, **Scheduled Scan**, and **Real-Time Processing**. Each type offers distinct configurations and capabilities to ensure effective file management.

## [1. On-Demand Scan](/docs/mdss/operations/scanning#1-on-demand-scan)

The On-Demand Scan allows you to initiate an instant scan of your selected storage. Here’s how it works:

- **Input Scan Name**: Provide a name for your scan.
- **Set Priority**: Choose the priority level for the scan.
- **Choose partition** (optional): Specify a path from the storage root to scan instead of the integrated folder path.
- **Select Workflow**: Choose your preferred workflow (you can preview it's configuration).
- **Start the Scan**: Click "Add Scan" to begin processing all files in your storage integration immediately.

## [2. Scheduled Scan](/docs/mdss/operations/scanning#2-scheduled-scan)

The Scheduled Scan enables you to set up recurring scans at specified intervals. You can configure the scan with the following options:

- **Input Scan Name**: Provide a name for your scan.
- **Set Priority**: Choose the priority level for the scan.
- **Choose partition** (optional): Specify a path from the storage root to scan instead of the integrated folder path.
- **Select Workflow**: Choose your preferred workflow.
- **Recurrence Options:** You can configure the scan to recur in one of four ways:

  - **Per-minute**: Set the scan to trigger every specified number of hours. The scheduling begins immediately upon clicking "Schedule Scan."
  - **Daily**: Configure the scan to recur every specified number of days, starting from the moment you click "Schedule Scan."
  - **Hourly**: Set the scan to trigger every specified number of hours. The scheduling begins immediately upon clicking "Schedule Scan."
  - **Daily**: Configure the scan to recur every specified number of days, starting from the moment you click "Schedule Scan."
  - **Weekly**: Set the scan to run every specified number of weeks, with the option to select the specific day of the week. The scan will commence at the time you click the button.
  - **Monthly**: Choose the frequency in months for the scan to repeat, along with the specific day of the month it will run.
- **Avoid concurrent schedule runs -** When enabled, the system will skip a scheduled scan run if the previous run is still in progress. This prevents multiple scans from running simultaneously.

## [3. Real-Time Processing](/docs/mdss/operations/scanning#3-real-time-processing)

Real-Time Processing continuously monitors your storage integration for any new or modified files after the scan has started. This option includes:

- **Input Scan Name**: Provide a name for your scan.
- **Set Priority**: Choose the priority level for the scan.
- **Choose partition** (optional): Specify a path from the storage root to scan instead of the integrated folder path. Only one single Real-Time Processing scan is allowed per partition.
- **Choose monitoring date** (optional): By default only new files are picked starting from the moment real time processing is enabled. You can select a date from which the monitoring will start
- **Select Workflow**: Choose your preferred workflow.
- **Processing Methods**: You can select from two methods of Real-Time Processing:

  - **Polling Method**: This method checks for new files at specified intervals in the order of seconds.
  - **Event-Based Mode**: Available for certain storage integrations, this method allows you to configure a function that sends notifications to MetaDefender Storage Security via a generic webhook endpoint whenever a file is added to your storage For more information, check out this page [Event-based handling](/docs/mdss/configuration/event-based-handling).

## [Monitoring starting date](/docs/mdss/operations/scanning#monitoring-starting-date)

This feature will allow users to set a specific date in the past to start a real time processing.

Info

Retention configuration will alter this configuration on runtime to not process the same files after were removed from the report

## [Partition scanning](/docs/mdss/operations/scanning#partition-scanning)

Partitions replace the integrated folder path for that scan only. Any folder path configured during storage integration will be ignored. The partition path takes full effect instead. Partitions are defined relative to the root of the storage source, and this behavior is consistent across all supported storage types.

For example, if your integrated storage is `my-bucket/` and you want to scan only `my-bucket/folder/subfolder/`, your partition should be set to `folder/subfolder/`.

Info

For **OPSWAT MFT, OneDrive, SharePoint, Box and SharePoint OnPrem**: If no specific users or document libraries are selected, the integration applies to **all users/doc libraries**, and **every one of them must contain the specified folder** or the partition scan will fail.

## [Priority scanning](/docs/mdss/operations/scanning#priority-scanning)

MetaDefender Storage Security features a **Priority Scanning** system that allows you to assign priority levels to your scans, ensuring that critical tasks are processed more efficiently. This feature is available for all scan types, including On-Demand, Scheduled, and Real-Time Processing.

#### [Priority Scanning Behavior:](/docs/mdss/operations/scanning#priority-scanning-behavior)

While you can assign priority levels to any type of scan—On-Demand, Scheduled, or Real-Time Processing—it's important to understand that these priorities do not influence the execution order of scans. Here’s how it works:

- **Same Priority, Same Type**: If you have two On-Demand scans with the same priority, they will run concurrently without any prioritization.
- **Different Priorities, Same Type**: When two scans of the same type are initiated with different priorities, the scan with the higher priority will be processed faster, but they will still run concurrently.
- **Different Types, Different Priorities**: For scans of different types, such as a Real-Time scan with Low priority and a Scheduled scan with High priority, the priority level will still be respected. The Scheduled scan will be processed faster than the Real-Time scan, regardless of their types.

#### [Key Features of Priority Scanning:](/docs/mdss/operations/scanning#key-features-of-priority-scanning)

- **Priority Levels**: You can choose from three priority options—**High**, **Medium**, and **Low**—when initiating any scan.
- **Efficient Processing**: Scans with higher priority levels are processed faster than those with lower priority levels, allowing you to manage your resources effectively and address urgent tasks promptly.
- **Concurrent Scanning**: Multiple scans can run simultaneously at the same priority level, ensuring flexibility in your scanning operations.

By leveraging the Priority Scanning feature, you can enhance your file management processes and ensure that your most critical scans are prioritized effectively. This not only improves overall performance but also enhances the efficiency of your scanning operations. For more ways to fine-tune performance and customize your deployment for speed, please check out this page: [Performance Tuning Guide](/docs/mdss/configuration/performance-tuning-guide).

## [Scan Overlap Protection](/docs/mdss/operations/scanning#scan-overlap-protection)

MetaDefender Storage Security prevents two scans from running at the same time over the same physical storage location. The same location, regardless if it's a bucket, share, site, or folder, can be added to the product more than once (for example, a bucket root and a sub-folder within it, or the same location added twice with different credentials). Scanning both at once wastes resources by re-processing the same files and, when a tagging or remediation workflow is enabled, can create a repeating loop or unexpected behavior in general.

#### [Behavior](/docs/mdss/operations/scanning#behavior)

This check takes place before starting any type of scan (**On-Demand**, **Real-Time Processing** or **Scheduled**) and will check if the storage location you are trying to start a scan for overlaps with a storage location from any other running scan. If it does overlap, you will receive this error:

Currently, this overlap detection compares locations within the same storage protocol type. It does not detect overlap between two different protocols pointing at the same physical storage (for example, the same NAS accessed over two different protocols). Path comparison is also case-sensitive, so locations that differ only in letter case will not be recognized as overlapping.

#### [Skipping the scan overlap check](/docs/mdss/operations/scanning#skipping-the-scan-overlap-check)

Some environments intentionally rely on running scans over overlapping locations and may need to preserve that behavior. For these cases, the overlap check can be disabled using the environment variable:

- **Variable**: SKIP_SCAN_OVERLAP_CHECK
- **Values**: *true* / *false*
- **Default**: *false*
- **Effect**: When *false*, overlap protection is active and overlapping scans are blocked. When *true*, the overlap check is skipped entirely and all scans are allowed to start regardless of overlap.
