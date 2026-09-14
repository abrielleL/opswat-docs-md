<!-- source: https://www.opswat.com/docs/mddrive/process/results--management -->

# Results Management

### [Analyze Reports](/docs/mddrive/process/results--management#analyze-reports)

MetaDefender Drive comes with data visualization graphs and scan reports list, including:

- Visual representation of all the performed scans.
- Interactive charts for each performed scan.

A graphical representation of all scans run by a MetaDefender Drive

- Device and Date filters to customize the view based on devices and time periods.

Filtering scan reports by Device and Date

### [Rename Existing Reports](/docs/mddrive/process/results--management#rename-existing-reports)

When a scan is complete and its report is generated, it will be assigned a suggested name using the system details detected by MetaDefender Drive following this pattern: *"host name, brand name, scanned disk label"*

You can rename any report to easily recognize it later by clicking the **Pen icon:**

### [Create a Workflow Based on a Scan Configuration](/docs/mddrive/process/results--management#create-a-workflow-based-on-a-scan-configuration)

You can choose to add a new workflow based on your most recent scan parameters, including preferences and selected paths:

To save a workflow, click **Create a Workflow** then give it a name. The workflow name is also suggested using the target system's hostname/brand-name, similar to reports. The saved workflow will be stored under **Workflow** settings.

For more details about Workflows and how to use them, please refer to the [Using Workflows](https://docs.opswat.com/mddrive/process/processing-workflows) page.

### [Rescan and Detect Delta Change in Data](/docs/mddrive/process/results--management#rescan-and-detect-delta-change-in-data)

If there is a baseline set for a workflow, every time you select **Rerun** from the Workflows page or click **Run this scan again** from the Reports page.

MetaDefender Drive will compare every file under the path associated with the selected workflow to their baseline. The results will include a detailed report of the differences found.

For more details about Workflows and how to use them, please refer to the [Using Workflows](https://docs.opswat.com/mddrive/process/processing-workflows) page.

### [Save Reports in Different Formats](/docs/mddrive/process/results--management#save-reports-in-different-formats)

Once the report processing is complete, you will be prompted that a final report has been generated and its location on the NTFS */MetaDefender Drive* partition under */reports*.

Saving the report data to the external partition is necessary to ensure your data won't be lost once the target system is powered off and MetaDefender Drive is removed.

**You can save reports in four formats:** JSON (default), TXT, PDF and CSV.

Scan report saving options

### [Differential Scan Indicator in Reports](/docs/mddrive/process/results--management#differential-scan-indicator-in-reports)

If the scan was a differential scan, the saved JSON, TXT and PDF reports state this in their report summary.

### [Save Clean File Reports](/docs/mddrive/process/results--management#save-clean-file-reports)

By checking the **Clean File Reports** option, MetaDefender Drive will save a list of the clean files (with files' hash) in your MetaDefender Drive storage.

Info

Enabling the **Clean File Report** option will slow down the scan and increase allocated space from the drive storage.

A sample file report with files' hash

## [Sync Reports for Central Management](/docs/mddrive/process/results--management#sync-reports-for-central-management)

If MetaDefender Drive is configured with [OPSWAT Central Management](https://docs.opswat.com/ocm), you can sync your scan reports to be viewed from OPSWAT Central Management by clicking **Sync All Reports** in the reports section.

The Reports page showing the status of syncing reports with OPSWAT Central Management

Once all reports are synced, the status bar next to the **Sync all Reports** button will display the message *"All Reports Synced Successfully"*:

The Reports page showing the status after all reports have been synced with OPSWAT Central Management
