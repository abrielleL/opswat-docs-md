<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/sandbox/what-is-displayed-on-the-process-result-tile- -->

# What is displayed on the process result tile?

This article applies to MetaDefender Core 5.13.0 or higher

MetaDefender Core provides a quick overview of scan results using compact tiles that summarize results for each engine. This page explains the information displayed on the Adaptive Sandbox tile and details how the tile operates.

## [Successful scan](/docs/mdcore/v5.22.0/sandbox/what-is-displayed-on-the-process-result-tile-#successful-scan)

For successful scans, the tile displays the MetaDefender Aether fore Core (Adaptive Sandbox) verdict, the number of threat indicators, and the IOCs (Indicators of Compromise) identified during the scan. The tile's color corresponds to the verdict, providing a quick visual summary.

Clicking on the tile opens the detailed report, allowing users to review in-depth information about the scan results.

## [Failed scan](/docs/mdcore/v5.22.0/sandbox/what-is-displayed-on-the-process-result-tile-#failed-scan)

Failed scans are displayed with the error message "**Failed to process**". This indicates an issue with the scan, and users may need to check the system logs or settings for more details.

Clicking on the tile opens the error report, where users can review the error details to understand the cause of the failure.

## [Skipped scan](/docs/mdcore/v5.22.0/sandbox/what-is-displayed-on-the-process-result-tile-#skipped-scan)

Depending on the workflow configuration, the Sandbox scan might be skipped. In this case, the tile displays the message "**No specific configuration**" with a grey accent or "**Skipped due to no triggers**" , indicating that the scan was not configured to run.

| Skipped by MDCore | Skipped by Sandbox CDR workflow |
| --- | --- |
|  |  |
