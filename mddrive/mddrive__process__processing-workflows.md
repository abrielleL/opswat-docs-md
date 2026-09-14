<!-- source: https://www.opswat.com/docs/mddrive/process/processing-workflows -->

# Using Workflows

A MetaDefender Drive Workflow is a scan with a specific set of configurations to run on a specific device. It can be saved and run multiple times on the assigned device. MetaDefender Drive operators can also select a scan report as the baseline for a specific workflow to compare future scans. Workflows are designed to save time by simplifying rerunning scans and comparing and analyzing scan results.

For each target machine, if there were workflows saved from scan reports (please see [Results](https://www.opswat.com/docs/mddrive/process/results--management) article), under Workflow tab there will be a list of Workflows with a series of (maximum) 10 report snapshots associated to each workflow.

## [Report Baseline and Data Integrity Verification](/docs/mddrive/process/processing-workflows#report-baseline-and-data-integrity-verification)

You can also use the report snapshots to verify if your data has been altered by comparing them. You can select a specific snapshot to compare with all the following scan results by clicking **Mark as baseline** next to the selected report.

Info

A baseline report will be pinned at the top of the workflow it is assigned to. It won’t be deleted by choosing not to keep local reports after syncing with an OPSWAT Central Management server.

The **Workflows** page showing saved workflows and the scans performed using a specific workflow

You can **rename**, **delete**, or **run** a scan using any of your saved workflows by selecting the **Run** option from the workflow menu:

The workflow menu where you can run, rename, or delete a workflow
