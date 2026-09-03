<!-- source: https://www.opswat.com/docs/supply-chain/operating/jobs -->

# Jobs

The Jobs page is where you can monitor and manage all scanning activity in MetaDefender Software Supply Chain. It gives you a real-time view of the scans that are currently running, along with the scheduled scans that will run in the future. To open it, select **Jobs** from the left-side menu.

The page is organized into two sections: **Active Jobs** and **Upcoming Jobs**.

## Active Jobs

The Active Jobs table lists the jobs that are currently running. While at least one job is in progress, the table refreshes automatically every few seconds, so the displayed information is always up to date.

The table provides the following information:

- **Job Name:** the name given to the job when it was created. If no name was provided, the name of the scanned repository is displayed instead.
- **Status:** the current scanning state of the job.
- **Job Type:** how the job was triggered: Scan Now, Schedule, or Real-time.
- **Vulnerabilities:** the severity breakdown of the vulnerabilities found so far: Critical, High, Medium, Low, and Unknown.
- **Files Processed:** the number of files processed so far.
- **Connection:** the connection that the scanned repository belongs to.
- **Start Time:** the date and time when the scan started.

Click on a job to open its report and follow the scan results in detail. You can also use the search field to find a specific job by name.

To cancel a running job, click the cancel button at the end of its row and confirm your choice in the **Cancel Job** dialog. When a job finishes, a **Job Completed** notification is displayed, with a direct link to view its report.

## Upcoming Jobs

The Upcoming Jobs table lists the scheduled jobs that have not started yet:

- **Job Name:** the name given to the job when it was created.
- **Job Frequency:** how often the job runs: Hourly, Daily, Weekly, or Monthly.
- **Connection:** the connection that the job will scan.
- **Starts In:** the time remaining until the next run.
- **Scheduled Date & Time:** the exact date and time of the next run.

To remove a scheduled job, click the delete button at the end of its row and confirm your choice in the **Delete Job** dialog.

## Creating a New Job

Click the **Create Job** button in the upper-right corner of the page to open the New Job panel, then choose one of the three available job types:

- **Scan Now:** starts a one-time scan immediately.
- **Schedule Scan:** runs the scan on a recurring schedule - hourly, daily, weekly, or monthly. Scheduled jobs are displayed in the Upcoming Jobs table until they start.
- **Real-Time Scan:** continuously monitors the selected repositories and automatically scans new content as it appears.

After selecting the job type, choose the connection, the repositories and branches to be scanned, the workflow to apply, and the priority of the job. Optionally, you can also give the job a custom name.

If the Create Job, Cancel, or Delete buttons are disabled with the message "This action is restricted due to license limitations", your current license does not allow job actions. You can review your license on the Settings page.
