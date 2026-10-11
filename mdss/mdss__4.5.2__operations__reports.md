<!-- source: https://www.opswat.com/docs/mdss/4.5.2/operations/reports -->

# Reports

After a process is finished a report is produced for you by MetaDefender Storage Security. This report has information about the overall scan of your storage (i.e. the number of detected issues) as well as individual file analysis details.

You can access all the reports generated for a specific storage by navigating from the left menu:

![](https://uploads.developerhub.io/prod/k8zL/atd4nm5l7hvuuok8zd4vqhm4dx6dw8tb91cf84d0fpdioalq61jk8i3mw0tltln7.png)

Here are some actions that are available for you:

- Search for a report or filters report based on type or a specific time range
- Click on a report in order to see more details and you will be redirected to the report page
- Delete a report using the three dots menu from the last column

#### Scan Report

![](https://uploads.developerhub.io/prod/k8zL/ffqcadnl1rvp1ktseh2a646vw7lugiv1yis9gbdi4xi8r1a82iy3fenj0up9ualt.png)

#### Real Time Processing Report

![](https://uploads.developerhub.io/prod/k8zL/4hmsf5r9tuuxi62mb4oty1rtlxlqeu0thqud55znbuuc09ybl17ldfg1b4verxdn.png)

> **Info**
>
> Cleaning a RTP report will not reprocess existing files.
>
> In case one of the following, on cleaning the RTP report only the files that were not processed will be handled.
>
> **DISCOVERY_SERVICE _SMB_RTP_HANDLING=1**
>
> **DISCOVERY_SERVICE_SFTP_RTP_HANDLING=1**
>
> **DISCOVERY_SERVICE_NFS_RTP_HANDLING=1**
>
> **DISCOVERY_SERVICE_FTP_RTP_HANDLING=1**

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
