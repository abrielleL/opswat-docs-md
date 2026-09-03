<!-- source: https://www.opswat.com/docs/mdss/operations/reports -->

# Reports

After a process is finished a report is produced for you by MetaDefender Storage Security. This report has information about the overall scan of your storage (i.e. the number of detected issues) as well as individual file analysis details.

You can access all the reports generated for a specific storage by navigating from the left menu:

Here are some actions that are available for you:

- Search for a report or filters report based on type or a specific time range
- Click on a report in order to see more details and you will be redirected to the report page
- Delete a report using the three dots menu from the last column

#### [Scan Report](/docs/mdss/operations/reports#scan-report)

#### [Real Time Processing Report](/docs/mdss/operations/reports#real-time-processing-report)

Info

Cleaning a RTP report will not reprocess existing files.

In case one of the following, on cleaning the RTP report only the files that were not processed will be handled.

**DISCOVERY_SERVICE _SMB_RTP_HANDLING=1**

**DISCOVERY_SERVICE_SFTP_RTP_HANDLING=1**

**DISCOVERY_SERVICE_NFS_RTP_HANDLING=1**

**DISCOVERY_SERVICE_FTP_RTP_HANDLING=1**
