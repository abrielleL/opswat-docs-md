<!-- source: https://www.opswat.com/docs/mdss/4.6.0/operations/reprocess-files -->

# Reprocess files

MetaDefender Storage Security allows users to manually initiate a new scan for files. This feature provides control and flexibility, enabling rescans for the following scenarios:

- Investigating potential false positives
- Re-evaluating a file after anti-malware definition updates
- Re-processing a file after a policy configuration change
- Attempting to scan an encrypted file by providing the correct password(s)

Files can be rescanned using either the **graphical user interface (GUI)** or the **Application Programming Interface (API)**.

> **Info**
>
> Reprocess actions have been designed for finished scans and are not applicable to running scans or active Real-Time Processing (RTP) scans.

## Using the Report Reprocess Flow

You can initiate a batch rescan directly from the MetaDefender Storage Security web interface:

1. From the scan report, go to **Actions -> Re-Scan Now**

![](https://uploads.developerhub.io/prod/k8zL/sh9ss4jfl2cooaavvvsmbcyotty9tk8y9wk5ap5khm0ut6bjq4gzus56kuwrjh8x.png)

2. Configure the reprocess filters with the desired  **Status**, **Detection**, and **Workflow** to be used by the rescan action.

![]()

3. After a batch rescan, the files of the report can be filtered by the Workflow and Date of the rescan action.

![](https://uploads.developerhub.io/prod/k8zL/oiptdtf1jpbq6u3fazbg93kefxy76tbq2t55s76hnu1zq198149zuvxz8rkum7m7.png)

> **Info**
>
> The rescan process will filter for files that match both the STATUS and the DETECTION filters.
>
> Adding multiple DETECTION filters will scan will filter for files that match ALL DETECTIONS and not at least one of them.

Rescanning for **Blocked** files with **Sensitive Data -** **AND - Vulnerabilities** will not rescan any files because no files have triggered both **DLP** and **Vulnerability** detection flags in the scenario above.

![](https://uploads.developerhub.io/prod/k8zL/8z27s4agkl1clehp2s17nogppxwd09yrmkph6x72nqsic4urbz4s380hdqkry5i3.png)

> **Info**
>
> Reprocessing for Allowed and Blocked files will reprocess all files with Allowed and Blocked files but not any with Failed Remediations or other results.

![](https://uploads.developerhub.io/prod/k8zL/bskzhcfdarhpmk5kxfk2nu0znebc16mjayestmo5s3a2guqwf31eya717tq29m56.png)

> **Warning**
>
> Allowed and Blocked file results are 1 tier above Failed, Failed Remediations, and Canceled file results.
>
> Reprocessing for Allowed and Failed Remediations Files will NOT rescan Blocked files with Failed Remediation results because the rescan did not target Blocked files. Only Allowed files, with or without Failed Remediations, will be reprocessed.

![](https://uploads.developerhub.io/prod/k8zL/gobhb1k73u9a8x7i36dqs8616y31em0w69lrrvuuq02y7i2be68j19o86xy55v9n.png)

![](https://uploads.developerhub.io/prod/k8zL/fmzs9c2yogf4cqnxhm3gn8y8tm1v2mxqyc2ymho31p4j3wfznbpj4wf8xcff4lfx.png)

> **Info**
>
> Reprocessing for ONLY Failed Remediation files will reprocess both Allowed and Blocked files that have Failed Remediations

![](https://uploads.developerhub.io/prod/k8zL/ik7ge90t69626dygrbsfrypbb84x4kzma0h98b5j1cytor04rsajnd7kka5xbkg6.png)

## Using the Reports GUI

You can initiate a single file rescan directly from the MetaDefender Storage Security web interface:

1. Navigate to the **Active Scans** page or the **Reports** page.
2. Locate the specific file you wish to rescan within the list (status is indicated by icons or labels).
3. Click the **Reprocess File** button in the actions column for the blocked or failed file. For encrypted files, click the lock icon, enter the passwords, and click the rescan icon.
4. The file will be re-queued for processing using the currently applicable workflow.
5. Monitor the scan progress and final result on the Reports page.

![](https://uploads.developerhub.io/prod/k8zL/j787sjof6s5mq9mmu6z7qwqc5n4zxmes4c2c4u74p2f984kzuvy79t17vhxysy14.png)

## Using the API

1. Files can be programmatically submitted for rescan using [this API](https://www.opswat.com/docs/mdss/metadefender-storage-security-api/ref#file-ondemandscan) from the MetaDefender Storage Security API. This is useful for automation or integration with other systems.
2. You will need the unique identifier (`fileId`) of the blocked file you wish to rescan. This ID can typically be retrieved from scan reports or event logs associated with the initial block action.
3. **Missing Information :** the specific endpoint for triggering a rescan of any blocked file in MDSS based on `fileId` should be documented here / link to it
4. Send an API request (POST) to the determined endpoint. The request body should be in JSON format (below)
5. The API should return a response indicating whether the rescan request was successfully submitted (a success message, perhaps a new `data_id` or task ID for tracking or whatever it is). The actual scan results will be available asynchronously and can be retrieved via subsequent API calls or viewed in the GUI.

**For standard rescan**

```json
{
	"fileId": "{string}",
	"scanId": "{string}",
	"storageProtocolType": "{int32}",
}
```

**For encrypted blocked files**

```json
{
	"fileId": "{string}",
	"scanId": "{string}",
	"storageProtocolType": "{int32}",
	"passwords": ["password_1","password_2"]
}
```

[Full API documentation](https://docs.opswat.com/mdss/metadefender-storage-security-api#file-ondemandscan) is available to guide your implementation.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
