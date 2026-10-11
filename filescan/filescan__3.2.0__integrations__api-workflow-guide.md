<!-- source: https://www.opswat.com/docs/filescan/3.2.0/integrations/api-workflow-guide -->

# API Workflow Guide

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**API Workflow Guide for MetaDefender Aether** (previously known as MetaDefender Sandbox)

**1. Log in to your instance using the provided email address and initial password (the Aether API key should be also be provided, and it can be regenerated any time)**

Best practices

If you deployed your instance on-premise, then please check that the **MetaDefender Cloud Reputation API** [MetaDefender Cloud Reputation Service](/docs/filescan/3.2.0/integrations/reputation-api-integration) is configured correctly on your instance!

This is highly recommended to get the most accurate verdict and a more comprehensive scan report!

**2. Browse the Sandbox API documentation at:**

a. <https://www.filescan.io/api/docs> (some endpoints will only be displayed when logged in)

b. Feel free to use the “Try it out” feature for any endpoints.

<https://docs.opswat.com/filescan/metadefender-sandbox-api-reference>

**3. Suggested API workflow:**

**a.** Calculate the SHA-256 hash of your sample and call the Sandbox Reputation API:

<https://docs.opswat.com/filescan/metadefender-sandbox-api-reference#get-reputation-hash-api-reputation-hash-get>

*Example request:*

CurlCopycurl -X 'GET' \
https://www.filescan.io/api/reputation/hash?sha256={hash}' \
-H 'accept: application/json' \
-H 'X-Api-Key: {your-key}'Success

Make sure the reputation feature is enabled if you are using a local instance. See: <https://docs.opswat.com/filescan/integrations/reputation-api-integration>

If the `overall_verdict` in the response is `likely_malicious` or `malicious`, then skip the next steps.

More information about Sandbox verdicts: [Report Verdict](/docs/filescan/3.2.0/datasheet/verdict)

**b.** Submit the file for analysis using the Scan File API: <https://docs.opswat.com/filescan/metadefender-sandbox-api-reference#scan-file-api-scan-file-post>

*Example request:*

CurlCopycurl -X 'POST' \
'https://www.filescan.io/api/scan/file' \
-H 'accept: application/json' \
-H 'X-Api-Key: {your-key}'
-H 'Content-Type: multipart/form-data' \
-F 'is_private=true' \
-F 'file=@{filename}'

*Example response* (note the `flow_id` field):

Flow_idCopy{
"flow_id": "6478f7d699da9635873cb7b4",
"priority": {
"applied": 100,
"max_possible": 100
}
}

**c.** Poll the `/api/scan/{flow_id}/report` API endpoint using the `flow_id` obtained in the previous step. The recommended polling frequency is 2 seconds.

*Example request:*

CurlCopycurl -X 'GET' \
'https://www.filescan.io/api/scan/6478f7d699da9635873cb7b4/report?filter=general&filter=overallState&filter=finalVerdict&other=' \
-H 'accept: application/json' \
-H 'X-Api-Key: {your-key}'

*Example Response:*

ExampleCopy{
"flowId": "6478f7d699da9635873cb7b4",
"allFinished": true,
"allFilesDownloadFinished": true,
"reportsAmount": 1,
"priority": "medium",
"pollPause": 5,
"fileSize": 68,
"reports": {
"ab6647f6-132a-4a6b-ad82-dfe01daee4a8": {
"overallState": "success",
"finalVerdict": {
"verdict": "NO_THREAT",
"threatLevel": 0.1,
"confidence": 1,
"verdictLabel": "no_threat_detected"
},
"file": {
"name": "fix-plasma.sh",
"hash": "c7c3cf68fbdbdb1d36759f853c8c9f3aa7eebcdd03fd24adc1e4eb2baa492ec5",
"type": null
},
"filesDownloadFinished": true,
"created_date": "06/01/2023, 19:56:09"
}
}
}

If the `allFinished` field is `true`, the scan can be considered complete. If the `overallState` is `success` or `success_partial`, then `finalVerdict.verdict` will contain the actual verdict for the sample. If the scan failed for some reason, it is recommended to retry the scan operation for this sample.

### [Special case for archives](/docs/filescan/3.2.0/integrations/api-workflow-guide#special-case-for-archives)

If the submitted file was an archive, the response will also contain a `sourceArchive` object and it is recommended to check the `sourceArchive.verdict` field to get a derived verdict that applies to the whole archive. For example:

JSONCopy{
"flowId": "6491f25290d361a9ad12fab2",
"allFinished": true,
"allFilesDownloadFinished": true,
"reportsAmount": 1,
"priority": "max",
"pollPause": 5,
"fileSize": 3881,
"sourceArchive": {
...
"verdict": "no_threat"
},
"reports": {...}
}

**d.** If more information is needed about a given analysis, then the `/api/scan/{flow_id}/report` API endpoint can be queried using additional filters (e.g. `allTags`, `allSignalGroups`). This extended query can return a substantially larger JSON:

JsonCopycurl -X 'GET' \
'https://www.filescan.io/api/scan/6478f7d699da9635873cb7b4/report?filter=general&filter=overallState&filter=finalVerdict&filter=allTags&filter=allSignalGroups&sorting=allSignalGroups%28description%3Aasc%2CaverageSignalStrength%3Adesc%29&sorting=allTags%28tag.name%3Aasc%29&other=' \
-H 'accept: application/json' \
-H 'X-Api-Key: {your-key}'

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
