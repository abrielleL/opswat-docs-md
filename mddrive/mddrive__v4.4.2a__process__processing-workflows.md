<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/process/processing-workflows -->

# Using Workflows

A MetaDefender Drive Workflow is a scan with a specific set of configurations to run on a specific device. It can be saved and run multiple times on the assigned device. MetaDefender Drive operators can also select a scan report as the baseline for a specific workflow to compare future scans. Workflows are designed to save time by simplifying rerunning scans and comparing and analyzing scan results.

Workflows can be created from the scan result pages (please refer to the [Scan Results](https://docs.opswat.com/mddrive/process/scan---results) and [Results Management](https://docs.opswat.com/mddrive/process/results--management) pages). On the **Workflow** page, you will find a list of the saved workflows, each workflows includes **10 reports report snapshots** associated with it. The report snapshots visualize how the scans data looked over time.

## [Report Baseline and Data Integrity Verification](/docs/mddrive/v4.4.2a/process/processing-workflows#report-baseline-and-data-integrity-verification)

You can also use the report snapshots to verify if your data has been altered by comparing them. You can select a specific snapshot to compare with all the following scan results by clicking **Mark as baseline** next to the selected report.

Info

A baseline report will be pinned at the top of the workflow it is assigned to. It won’t be deleted by choosing not to keep local reports after syncing with an OPSWAT Central Management server.

The **Workflows** page showing saved workflows and the scans performed using a specific workflow

You can **rename**, **delete**, or **run** a scan using any of your saved workflows by selecting the **Run** option from the workflow menu:

The workflow menu where you can run, rename, or delete a workflow
