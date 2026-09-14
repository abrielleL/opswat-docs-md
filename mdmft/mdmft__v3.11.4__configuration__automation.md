<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/automation -->

# Automation

Summarize Page    Connect to Cursor Connect to VS Code

On the Automation page, users with read access to Automated Jobs or MFT to MFT can view file transfer automations configured in *MetaDefender Managed File Transfer™*, visualized as a flow diagram. Users with the required permissions can also create and edit automations directly from this interface.

The central node in the flow diagram always represents the current MetaDefender Managed File Transfer™ instance.

- Inbound flows come from Automated Jobs
- Outbound flows go to Destinations or MFT to MFT connections

For a full introduction see:

- [MFT Integration](/docs/mdmft/v3.11.4/integrations/mft-integrations)
- [Introduction to File Transfer Automation](/docs/mdmft/v3.11.4/automated-file-transfer/automated-jobs)

Info

Automated Jobs are user-specific and can only be accessed and viewed by the user who created them. They are not shared with other users. System Administrators, however, can view all Automated Jobs to maintain a complete overview of the system’s configured automations.

### [Automation Tour](/docs/mdmft/v3.11.4/configuration/automation#automation-tour)

Guides you through the Automation page interface and highlights foundational information about Automated Jobs and MFT-to-MFT integration. The tour starts automatically when you first use this feature. Once you complete or skip the tour, it won't appear again unless you close the browser tab or log out and back in. You can restart the tour at any time by clicking the "Start Automation Tour" button.

It starts with a video

Start the tour on-demand

### [Managing Automations](/docs/mdmft/v3.11.4/configuration/automation#managing-automations)

To add a new Automated Job or MFT to MFT Destination, click the plus (+) button in the top-left corner of the flow diagram canvas and select the desired option.

Both actions open the familiar Manage dialog, where you can enter the required information.

Each automation node includes a three-dot menu for common management tasks, such as editing or removing the automation.

An automated job's menu

A Destination MFT's menu

Info

Fullscreen mode is view-only; to make changes, exit fullscreen first.

Transfer policy for MFT to MFT destinations can also be configured by clicking the rhombus icon on the connection line between the central MFT and the destination MFT.

Info

Automated Jobs with the same integration and job direction (Pull or Push) are grouped together. Groups can be expanded by selecting the icon on the node. Individual node connections are hidden when the group is collapsed.

Expanded Automated Job group

### [Filter Automations](/docs/mdmft/v3.11.4/configuration/automation#filter-automations)

File transfer automations can be filtered by Automation Type (MFT-to-MFT, My Automated Jobs, Created By Others), Job Direction (Pull, Push), Job Integration (SFTP, SMB, SPO, MFT), and Job Status (Enabled, Disabled, Incomplete). Filtering by these criteria helps administrators more easily review and manage automations.

Info

System administrators are able to view every Automated Job available in MetaDefender Managed File Transfer™ by using the Automation Type's Created by others filter.

### [Latest Automated Job Executions](/docs/mdmft/v3.11.4/configuration/automation#latest-automated-job-executions)

The Automated Job Executions widget displays the latest ten executions for each automated job. It shows the current status of a job, including whether it is running, completed successfully, or failed. This allows administrators and automation coordinators to quickly monitor recent activity and identify potential issues without navigating away from Automation page.
